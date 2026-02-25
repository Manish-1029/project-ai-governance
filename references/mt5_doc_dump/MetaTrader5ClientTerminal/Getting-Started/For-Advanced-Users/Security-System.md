[🏠 Document Start](../../README.md) / [Getting Started](../../Getting-Started.md) / [For Advanced Users](../For-Advanced-Users.md) / Security System

[Previous](Mailbox.md) | [Next](Live-Update.md)

# Security System

Particular attention is paid to the security of the trading platform. The following measures are undertaken to provide secure operation:

  * Data Encryption  
Data exchange between the trading platform and the server is compressed and encrypted based on 128-bit keys.
  * Extended Authentication  
The [extended authentication](Extended-Authentication.md) mode can be enabled on the server, which additionally improves account protection from unauthorized access.
  * Server Authentication  
During [authentication](../Connect-to-an-Account.md), not only clients confirm their authenticity, but the trade server also undergoes authentication in the trading platform. This is to ensure that the trade server is the very server, which it claims to be.
  * Protection of Configuration Files  
Connecting to a trade server using configuration files copied from the [/Config (#config)](Files-and-Folders.md#config) folder of another platform is impossible. All configuration files that store server connection settings and accounts are encrypted.
  * Protection of Passwords  
All password entering fields are protected from being viewed using hacking programs.



## Security of Databases

All databases of the platform are encrypted and protected from use on other platforms.

> Always keep account details in a safe place. If you move a platform from one computer to another, there is no possibility to use the information stored in it (accounts, emails, trade history). After authenticating on a server using an account, trade, mail and news databases are restored, but the account details can only be restored by contacting a broker.

  * Account Database  
The database of [accounts](../Open-an-Account.md) ([/Config/accounts.ini (#accounts)](Files-and-Folders.md#accounts)) of a platform is bound to a user account in the operating system and computer configuration. If a user tries to authorize in the platform under a different user account in the operating system, or when the platform data are transferred to another computer, the entire database of accounts is deleted during the start of the platform. In this connection, you must keep the accounts details (login and password) in a separate safe place.
  * Information Databases  
Mail, [trade (#trade-history)](../../Trading-Operations/Executing-Trades.md#trade-history) and symbol databases are encrypted. They are automatically deleted at an attempt to move them and open in a different platform.


