---
ms.date: 06/11/2020
keywords: powershell,командлет
title: Вопросы обеспечения безопасности при удаленном взаимодействии PowerShell с использованием WinRM
description: В этом документе рассматриваются вопросы безопасности и рекомендации по использованию удаленного взаимодействия PowerShell.
ms.openlocfilehash: 48167bd297905883b3d75caf9a07d06e6a9fc467
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "92501479"
---
# <a name="security-considerations-for-powershell-remoting-using-winrm"></a>Вопросы обеспечения безопасности при удаленном взаимодействии PowerShell с использованием WinRM

Удаленное взаимодействие PowerShell — это рекомендуемый способ управления системами Windows. В Windows Server 2012 R2 удаленное взаимодействие PowerShell включено по умолчанию. В этом документе рассматриваются вопросы безопасности и рекомендации по использованию удаленного взаимодействия PowerShell.

## <a name="what-is-powershell-remoting"></a>Что такое удаленное взаимодействие PowerShell?

Функция удаленного взаимодействия PowerShell использует службу [удаленного управления Windows (WinRM)](/windows/win32/winrm/portal), которая является реализацией протокола [веб-служб для управления (WS-Management)](https://www.dmtf.org/sites/default/files/standards/documents/DSP0226_1.2.0.pdf), чтобы дать пользователям возможность использовать команды PowerShell на удаленных компьютерах. Дополнительные сведения об использовании удаленного взаимодействия PowerShell можно найти в статье [Выполнение удаленных команд](running-remote-commands.md).

Удаленное взаимодействие PowerShell отличается от выполнения командлета с параметром **ComputerName** для запуска на удаленном компьютере, когда в качестве базового протокола используется удаленный вызов процедур (RPC).

## <a name="powershell-remoting-default-settings"></a>Параметры удаленного взаимодействия PowerShell по умолчанию

Удаленное взаимодействие PowerShell (и WinRM) прослушивают следующие порты:

- HTTP — 5985;
- HTTPS — 5986.

По умолчанию функция удаленного взаимодействия PowerShell допускает подключения только от участников группы "Администраторы".
Сеансы запускаются в контексте пользователя, поэтому все элементы управления доступом операционной системы, примененные к отдельным пользователям и группам, продолжают применяться к ним при подключении через удаленное взаимодействие PowerShell.

В частных сетях правило брандмауэра Windows по умолчанию для удаленного взаимодействия PowerShell принимает все подключения. В общедоступных сетях правило брандмауэра Windows по умолчанию допускает подключения удаленного взаимодействия PowerShell только из той же подсети. Необходимо явно изменить это правило, чтобы открыть удаленное взаимодействие PowerShell для всех подключений в общедоступной сети.

> [!Warning]
> Правило брандмауэра для общедоступных сетей предназначено для защиты компьютера от потенциально вредоносных попыток внешних подключений. Будьте внимательны при удалении этого правила.

## <a name="process-isolation"></a>Изоляция процессов

Функция удаленного взаимодействия PowerShell использует WinRM для обмена данными между компьютерами. WinRM выполняется как служба с учетной записью сетевой службы и порождает изолированные процессы, выполняющиеся как учетные записи пользователей, для размещения экземпляров PowerShell. Экземпляр PowerShell, выполняющийся как один пользователь, не имеет доступа к процессу, в котором выполняется экземпляр PowerShell от имени другого пользователя.

## <a name="event-logs-generated-by-powershell-remoting"></a>Журналы событий, создаваемые удаленным взаимодействием PowerShell

Компания FireEye опубликовала хорошую сводку журналов событий и других свидетельств безопасности, создаваемых в сеансах удаленного взаимодействия PowerShell, в статье [Investigating PowerShell Attacks](https://www.fireeye.com/content/dam/fireeye-www/global/en/solutions/pdfs/wp-lazanciyan-investigating-powershell-attacks.pdf).

## <a name="encryption-and-transport-protocols"></a>Протоколы шифрования и транспорта

Рекомендуется оценивать безопасность подключения удаленного взаимодействия PowerShell с двух точек зрения — начальной аутентификации и текущего обмена данными.

Независимо от используемого транспортного протокола (HTTP или HTTPS), WinRM всегда шифрует все удаленное взаимодействие с PowerShell после начальной проверки подлинности.

### <a name="initial-authentication"></a>Начальная проверка подлинности

Проверка подлинности используется для идентификации клиента для сервера и, в идеале, сервера для клиента.

Когда клиент подключается к серверу домена по имени компьютера, по умолчанию используется протокол аутентификации [Kerberos](/windows/win32/secauthn/microsoft-kerberos). Kerberos гарантирует идентификацию пользователя и сервера без отправки каких-либо повторно используемых учетных данных.

Если клиент подключается к серверу домена по IP-адресу (или подключается к серверу рабочей группы), проверка подлинности Kerberos невозможна. В этом случае удаленное взаимодействие PowerShell использует [протокол аутентификации NTLM](/windows/win32/secauthn/microsoft-ntlm). Протокол аутентификации NTLM гарантирует идентификацию пользователя без отправки каких-либо делегируемых учетных данных. Для подтверждения личности пользователя протокол NTLM требует, чтобы клиент и сервер вычисляли сеансовый ключ на основе пароля пользователя без передачи самого пароля. Серверу, как правило, неизвестен пароль пользователя, поэтому он связывается с контроллером домена, которому пароль пользователя известен и который вычисляет сеансовый ключ для этого сервера.

Протокол NTLM, однако, не гарантирует идентификацию сервера. Как и в случае с любыми протоколами, использующими NTLM для аутентификации, злоумышленник, имеющий доступ к учетной записи компьютера, присоединенного к домену, может заставить контроллер домена вычислить сеансовый ключ NTLM, тем самым олицетворяя сервер.

Проверка подлинности на основе NTLM отключена по умолчанию, но ее можно разрешить, настроив SSL на целевом сервере или настроив параметр TrustedHosts службы WinRM в клиенте.

#### <a name="using-ssl-certificates-to-validate-server-identity-during-ntlm-based-connections"></a>Использование SSL-сертификатов для проверки удостоверения сервера во время NTLM-подключений

Поскольку протокол аутентификации NTLM не может гарантировать идентификацию целевого сервера (а только то, что ему уже известен ваш пароль), можно настроить на целевых серверах использование протокола SSL для удаленного взаимодействия PowerShell.
Назначение SSL-сертификата целевому серверу (если он выдан центром сертификации, которому также доверяет клиент) обеспечивает аутентификацию на основе NTLM, которая гарантирует идентификацию как пользователя, так и сервера.

#### <a name="ignoring-ntlm-based-server-identity-errors"></a>Пропуск ошибок идентификации сервера на основе NTLM

Если реализация развертывания SSL-сертификата на сервере для NTLM-подключений невозможна, отключить связанные ошибки идентификации можно, добавив сервер в список **TrustedHosts**. Обратите внимание, что добавление имени сервера в список **TrustedHosts** не должно рассматриваться как утверждение о надежности самих узлов, так как протокол аутентификации NTLM не может гарантировать, что подключение на самом деле выполняется к предполагаемому узлу. Параметр TrustedHosts следует рассматривать как список узлов, для которых требуется отключать ошибки, возникающие из-за невозможности проверить удостоверение сервера.

### <a name="ongoing-communication"></a>Текущий обмен данными

После завершения начальной проверки подлинности WinRM выполняет шифрование всех текущих подключений. При подключении по протоколу HTTPS протокол TLS используется для согласования шифрования при передаче данных.
При подключении по протоколу HTTP шифрование на уровне сообщений определяется исходя из изначального протокола проверки подлинности.

- Обычная проверка подлинности не обеспечивает шифрование.
- Проверка подлинности NTLM использует шифр RC4 со 128-битным ключом.
- Шифрование проверки подлинности Kerberos определяется `etype` в билете TGS. Это AES-256 в современных системах.
- В шифровании CredSSP используется набор шифров TLS, который был согласован в подтверждении связи.

## <a name="making-the-second-hop"></a>Выполнение второго перехода

По умолчанию удаленное взаимодействие PowerShell использует для проверки подлинности протокол Kerberos (по возможности) или NTLM. Оба эти протокола выполняют проверку подлинности на удаленном компьютере без отправки учетных данных. Это наиболее безопасный способ проверки подлинности, но поскольку удаленный компьютер не имеет учетных данных пользователя, он не может получать доступ к другим компьютерам и службам от имени пользователя. Эту ситуацию называют "проблемой второго прыжка".

Существует несколько способов избежать ее. Описание этих способов, а также преимущества и недостатки каждого из них см. в разделе [Выполнение второго прыжка при удаленном взаимодействии PowerShell](PS-remoting-second-hop.md).

## <a name="references"></a>Ссылки

- [Удаленное управление Windows (WinRM)](/windows/win32/winrm/portal)
- [Веб-службы для управления (WS-Management)](https://www.dmtf.org/sites/default/files/standards/documents/DSP0226_1.2.0.pdf)
- [Типы зашифрованных сообщений 2.2.9.1](/openspecs/windows_protocols/ms-wsmv/58421aa4-861a-4410-831a-c999f094cdb7)
- [Kerberos](/windows/win32/secauthn/microsoft-kerberos)
- [Протокол проверки подлинности NTLM](/windows/win32/secauthn/microsoft-ntlm)
- [Расследование атак через PowerShell](https://www.fireeye.com/content/dam/fireeye-www/global/en/solutions/pdfs/wp-lazanciyan-investigating-powershell-attacks.pdf)
