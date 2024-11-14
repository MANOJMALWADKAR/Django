# Define Configuration setting in settings.py

EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'smtp.gmail.com
EMAIL_PORT = 587
EMAIL_USE_TLS = True
EMAIL_HOST_USER = 'Your_EMAIL'
EMAIL_HOST_PASSWORD = 'YOUR_MAIL_PASSWORD'

* NOTE => Adding Email Password here is not secure so we Chave to add app password instead of Email Password

# Create App Password

- Go to google account > security
- Enable Two step verification
- In Two step verification go to App Password
- Add app name of our project app(authenticationdemoapp)
- It Generate password
- Add this password to EMAIL_HOST_PASSWORD

# Send Mail

- Import send_mail from django.

    subject = 'welcome ot udemy'
    message = 'hi welcome'

    send_mail(
            subject,
            message,
            settings.EMAIL_HOST_USER,
            [instance.email],               //here we get mail of user
            fail_silently = False
    )