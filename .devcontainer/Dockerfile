# Utilise l'image Python 3.9 slim comme base (image légère)
FROM python:3.9-slim

# Établit le répertoire de travail dans le conteneur
WORKDIR /app

# Copie le fichier requirements.txt d'abord pour optimiser le cache Docker
COPY requirements.txt .

# Installe les dépendances Python sans cache pour réduire la taille de l'image
RUN pip install --no-cache-dir -r requirements.txt

# Copie le reste de l'application
COPY service/ ./service/

# Crée un utilisateur non-root et change les permissions
RUN useradd --uid 1000 theia && \
    chown -R theia /app

# Passe à l'utilisateur non-root
USER theia

# Expose le port 8080 pour les connexions externes
EXPOSE 8080

# Commande de démarrage avec Gunicorn
CMD ["gunicorn", "--bind=0.0.0.0:8080", "--log-level=info", "service:app"]