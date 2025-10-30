@Library('ma-lib-partagee') _

import org.exemple.utils.MonUtilitaire

pipeline {
    agent any
    
    tools {
        maven 'Maven 3.9'  
    }
    
    stages {
        stage('Initialisation') {
            steps {
                script {
                    echo "=== Stage 1 : Initialisation ==="
                    def utils = new MonUtilitaire(this)
                    utils.saluer("Jenkins User")
                    def resultat = utils.faireQuelqueChose()
                    echo "Résultat: ${resultat}"
                }
            }
        }
        
        stage('Utiliser une fonction globale') {
            steps {
                script {
                    echo "=== Stage 2 : Test de fonction globale ==="
                    def resultat = autreFonction("Ceci est un test de fonction globale.")
                    echo "Résultat de autreFonction : ${resultat}"
                }
            }
        }
        
        stage('Utiliser une étape personnalisée') {
            steps {
                script {
                    echo "=== Stage 3 : Étape personnalisée ==="
                    monEtapePersonnalisee {
                        echo "Ceci est le contenu du bloc passé à monEtapePersonnalisee."
                        echo "On peut même appeler une fonction de la Shared Library ici :"
                        def utils = new MonUtilitaire(this)
                        utils.saluer("De l'intérieur de l'étape personnalisée")
                    }
                }
            }
        }
        
        stage('Démonstration avec Maven (optionnel)') {
            steps {
                script {
                    echo "=== Stage 4 : Test avec Maven (si pom.xml existe) ==="
                    // Cette étape est optionnelle et ne s'exécutera que si vous avez un pom.xml
                    if (fileExists('pom.xml')) {
                        echo "Fichier pom.xml détecté, compilation avec Maven..."
                        buildMaven(goals: 'clean compile')
                    } else {
                        echo "Pas de pom.xml trouvé, cette étape est ignorée."
                    }
                }
            }
        }
    }
    
    post {
        success {
            echo '✅ Pipeline terminé avec SUCCÈS !'
        }
        failure {
            echo '❌ Pipeline terminé en ÉCHEC.'
        }
        always {
            echo '🔚 Nettoyage terminé.'
        }
    }
}
