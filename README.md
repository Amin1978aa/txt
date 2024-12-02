import smtplib
from email.mime.text import MIMEText

# E-posta içeriği oluşturuluyor
msg = MIMEText("Hesabınıza dair önemli bir güvenlik uyarısı var. Lütfen hemen şifrenizi güncelleyin. http://example.com")

# Hedef telefon numarasına e-posta gönderimi
phone_number = '5551234567'  # Hedef kişinin telefon numarası
carrier_gateway = '@txt.att.net'  # Hedefin operatörüne ait SMS gateway adresi

# E-posta alıcı adresi
sms_gateway = phone_number + carrier_gateway
msg['From'] = "your_email@gmail.com"
msg['To'] = sms_gateway
msg['Subject'] = "Acil Güvenlik Uyarısı"

# Gmail SMTP sunucusu ile e-posta gönderme
server = smtplib.SMTP('smtp.gmail.com', 587)
server.starttls()
server.login("your_email@gmail.com", "your_password")
server.sendmail("your_email@gmail.com", sms_gateway, msg.as_string())
server.quit()
