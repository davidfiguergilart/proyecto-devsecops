pipeline {
    agent any
    stages {
        stage('Descargar Código') {
            steps {
                echo 'Clonando el repositorio...'
                git branch: 'desarrollo',  url: 'https://github.com/davidfiguergilart/proyecto-devsecops.git'
            }
        }
        stage('Construir Imagen (Build)') {
            steps {
                echo 'Construyendo el contenedor...'
                sh 'docker build -t mi-app-segura:latest .'
            }
        }
        stage('Análisis de Seguridad (Trivy)') {
            steps {
                echo 'Buscando vulnerabilidades CRÍTICAS...'
                // Si Trivy encuentra algo CRITICAL, devuelve error (exit 1) y para el pipeline
                sh 'docker run --rm -v /var/run/docker.sock:/var/run/docker.sock aquasec/trivy image --exit-code 1 --severity CRITICAL mi-app-segura:latest'
            }
        }
        stage('Despliegue en Producción (CD)') {
            steps {
                echo '¡Imagen limpia! Desplegando en el servidor...'
                // Paramos lo viejo si existe y lanzamos lo nuevo
                sh 'docker stop app-produccion || true'
                sh 'docker rm app-produccion || true'
                sh 'docker run -d --name app-produccion mi-app-segura:latest'
            }
        }
    }
}