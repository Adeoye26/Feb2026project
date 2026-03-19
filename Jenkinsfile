<<<<<<< HEAD
pipeline{A
=======
pipeline{
>>>>>>> 944c2dd (orobo)
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
	agent any
      stages{
           stage('Checkout'){
              steps{
		 echo 'cloning..'
<<<<<<< HEAD
                 git 'https://github.com/RayItern/JUNECLASSPRO1.git'
=======
                 git 'https://github.com/Adeoye26/Feb2026project.git'
>>>>>>> 944c2dd (orobo)
              }
          }
          stage('Compile'){
              steps{
                  echo 'compiling..'
                  sh 'mvn compile'
	      }
          }
          stage('CodeReview'){
              steps{
		    
		  echo 'codeReview'
                  sh 'mvn pmd:pmd'
              }
          }
          
          stage('Package'){
              steps{
                  sh 'mvn package'
              }
          }
      }
}

