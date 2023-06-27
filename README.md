import requests
import json

# Configuration
base_url = "https://api.choruspro.gouv.fr/v1"

# Informations d'authentification
client_id = "YOUR_CLIENT_ID"
client_secret = "YOUR_CLIENT_SECRET"
username = "YOUR_USERNAME"
password = "YOUR_PASSWORD"

# Obtenir un jeton d'accès
def get_access_token():
    auth_url = base_url + "/oauth2/token"
    headers = {"Content-Type": "application/x-www-form-urlencoded"}
    data = {
        "grant_type": "password",
        "client_id": client_id,
        "client_secret": client_secret,
        "username": username,
        "password": password
    }
    response = requests.post(auth_url, headers=headers, data=data)
    if response.status_code == 200:
        return response.json()["access_token"]
    else:
        raise Exception("Échec de l'obtention du jeton d'accès")

# Créer une facture
def create_invoice(access_token, invoice_data):
    create_invoice_url = base_url + "/invoices"
    headers = {
        "Authorization": "Bearer " + access_token,
        "Content-Type": "application/json"
    }
    response = requests.post(create_invoice_url, headers=headers, data=json.dumps(invoice_data))
    if response.status_code == 201:
        return response.json()
    else:
        raise Exception("Échec de la création de la facture")

# Récupérer les détails d'une facture
def get_invoice_details(access_token, invoice_id):
    get_invoice_url = base_url + "/invoices/" + invoice_id
    headers = {
        "Authorization": "Bearer " + access_token,
        "Content-Type": "application/json"
    }
    response = requests.get(get_invoice_url, headers=headers)
    if response.status_code == 200:
        return response.json()
    else:
        raise Exception("Échec de la récupération des détails de la facture")

# Exemple d'utilisation
access_token = get_access_token()

# Créer une facture
invoice_data = {
    "invoice_number": "INV-001",
    "customer_name": "John Doe",
    "amount": 100.0,
    "currency": "EUR",
    # Autres données de facture...
}
invoice = create_invoice(access_token, invoice_data)
print("Facture créée avec succès. ID de facture:", invoice["invoice_id"])

# Récupérer les détails d'une facture
invoice_id = invoice["invoice_id"]
invoice_details = get_invoice_details(access_token, invoice_id)
print("Détails de la facture:", invoice_details)
- 👋 Hi, I’m @fernandezemilie
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
fernandezemilie/fernandezemilie is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
