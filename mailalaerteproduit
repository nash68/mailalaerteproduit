import feedparser
import smtplib
from email.mime.text import MIMEText

# URL du flux RSS
rss_url = "https://rappel.conso.gouv.fr/rss"

# Votre adresse e-mail et mot de passe (pour l'envoi de l'e-mail)
sender_email = "votre_adresse_email@gmail.com"
sender_password = "votre_mot_de_passe"

# Adresse e-mail du destinataire
recipient_email = "nash68@gmail.com"

def get_new_items():
    # Récupère les derniers éléments du flux RSS
    feed = feedparser.parse(rss_url)
    return feed.entries

def send_email(subject, body):
    # Crée le message e-mail
    msg = MIMEText(body)
    msg["Subject"] = subject
    msg["From"] = sender_email
    msg["To"] = recipient_email

    # Envoie l'e-mail
    with smtplib.SMTP("smtp.gmail.com", 587) as server:
        server.starttls()
        server.login(sender_email, sender_password)
        server.sendmail(sender_email, recipient_email, msg.as_string())

if __name__ == "__main__":
    # Récupère les nouveaux éléments
    new_items = get_new_items()

    if new_items:
        for item in new_items:
            title = item.title
            link = item.link
            summary = item.summary

            # Envoie un e-mail pour chaque nouvel élément
            subject = f"Nouvel élément ajouté : {title}"
            body = f"Résumé : {summary}\nLien : {link}"
            send_email(subject, body)
            print(f"E-mail envoyé pour : {title}")
    else:
        print("Aucun nouvel élément trouvé dans le flux RSS.")
