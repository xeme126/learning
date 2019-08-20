
mvn clean package
mvn dependency:sources
mvn install:install-file "-Dfile=-xx-1.0.0.jar" "-DgroupId=com.xx.xx" "-DartifactId=xx-xx" "-Dversion=1.0.0" "-Dpackaging=jar" "-DgeneratePom=true"

