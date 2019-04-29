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
    
## Verify

Run stuff like findbugs/pmd checks:

    mvn verify

# Streams API

## map and sort a collection

```
List<Pair<Instant, Instant>> foo = sourceList
                        .stream()
                        .map(item -> Pair.of(item.getStart(), item.getEnd()))
                        .collect(Collectors.toList());
// sort by left element
foo.sort(Comparator.comparing(Pair::getLeft));
```

# Lambdas

## Inline sort a comparable class.

* Say of objects compare a list of objects with `Instant` property time. Use this to sort the objects by time:

```
List<TimeObject> positions = ...;
positions.sort(Comparator.comparing(pos -> pos.getTime()));
```

# Gradle

## force re-build steps

    ./gradlew test --rerun-tasks
    
## verbose output

    -i

## show stdout / stderr on tests

Add to the `build.gradle` file

```
test {
    testLogging {
        showStandardStreams = true
        events = ['standard_out', 'standard_error']
    }
}
```
