# Maven

## Only build/test single module:

    mvn test -pl modulename

## Only test a single class

(You don't have to include the full path)

    mvn test -Dtest=TestClassName

## Skip tests

    mvn install -DskipTests

or

    mvn install -Dmaven.test.skip=true

## Execute class in maven

    mvn compile exec:java -Dexec.mainClass=com.foo.bar.MyMainClass -Dexec.args="arg1 arg2"
