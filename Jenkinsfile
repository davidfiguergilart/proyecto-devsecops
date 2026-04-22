pipeline {
    agent any
    stages {
        stage ('Descargar Código') {
            steps {
                echo 'Clonando el repositorio desde GitHub...'
                // Verifica que esta sea tu URL de repositorio
                git branch: 'desarrollo', url: '[https://github.com/davidfiguergilart/proyecto-devsecops.git](https://github.com/davidfiguergilart/proyecto-devsecops.git)'
            }
        }
        stage ('Construir Imagen Docker (Build)') {
            steps {
                echo 'Construyendo el contenedor seguro...'
                sh 'docker build -t mi-app-segura:latest .'
            }
        }
    }
}
