[🏠 Document Start](../../README.md) / [Getting Started](../../Getting-Started.md) / [For Advanced Users](../For-Advanced-Users.md) / Mailbox

[Previous](Manage-Trading-Accounts.md) | [Next](Security-System.md)

<a id="mailbox"></a>
# Mailbox (#mailbox)

The trading platform contains an internal mail system. It allows you to receive important information from your broker: information about open accounts, useful information about the platform features, upcoming events, etc.

All the emails are displayed in the Mailbox tab of the Toolbox window.

![Mail System](images/mail.png)

Email subject

Email sender's name

Email recipient's name

Email sending or receiving time

[Write an email (#create)](Mailbox.md#create)

Unread messages are marked with icon ![Unread message](images/mail_unread_icon.png), read ones - ![Read message](images/mail_read_icon.png). Outgoing emails are marked with icon ![Outgoing message](images/mail_outgoing_icon.png). When the function of response to an email is used, messages are joint into threads, which makes it easy to navigate in conversations with clients. Email threads are marked with icon ![Email Thread](images/mail_branch_icon.png). To expand a thread, click on this icon.

> Emails are stored on the trade server. When you delete an email from the platform interface, it will not be re-downloaded. However, if you delete the platform mail database (the file "/bases/server_name/mail/mail-account_number.dat") or connect from another platform, all the mails for the last 30 days will be downloaded again.

<a id="view"></a>
## Reading an Email (#view)

Double-click on an email to read it.

![To read an email, double-click on it in the list](images/mail_view.png)

The top of the email contains the following data: a client's account and name, date of email, its subject and attachments (if any).

The toolbar of this window contains the following commands:

  * ![Reply](images/mail_answer_icon.png) Reply — open email creation window with the field "To" filled in and a quote of a received email;
  * ![Save](images/save_icon.png) Save — save the email on a computer as a HTML file or a text file in Unicode standard;
  * ![Print](images/print_icon.png) Print — print the email;
  * ![Print preview](images/print_preview_icon.png) Print Preview — open the preview window before printing the email;
  * ![Attachment](images/mail_attachment_icon.png) Attachment — save files attached to the email. Another way to save an attachment is to click on its name in the appropriate field of the email header.



<a id="create"></a>
## Writing an Email (#create)

To create an email, select the appropriate command in the context menu, or use the hot key "Insert" on the Mailbox tab.

![Select the email recipient, add email subject and body](images/mail_create.png)

Specify the following data in this window:

  * To — the account of a trade server administrators you want to send an email to;
  * Subject — subject of the email;
  * Attachments — files attached to the email. To attach a file click ![Add attachment](images/add_attachment_button.png), and specify the desired file. To remove an attachment click ![Delete attachment](images/delete_attachment_button.png). If several files are attached to an email, they are deleted starting from the last one;
  * Below is the window for working with am email text. It contains three tabs: Edit, View and Source. In the Edit tab you can write an email text and use commands for working with it. You can view the final email in the View tab. The Source tab allows working with the source HTML code of an email.



> Note the following limitations on attachments:
