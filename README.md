# maven-flatten-bug
### Mini repo to reproduce bug in maven-flatten-plugin

When using `${revision}` or `${sha1}` in child module with `<flattenMode>resolveCiFriendliesOnly</flattenMode>`. They do not get replaced.

### Maven config
```
<properties>
    <sha1/>
    <revision>1.0.0</revision>
</properties>
```
```
...
<pluginManagement>
    <plugins>
        <plugin>
            <groupId>org.example</groupId>
            <artifactId>flatten-bug-plugin</artifactId>
            <version>${revision}${sha1}-SNAPSHOT</version>
        </plugin>
    </plugins>
</pluginManagement>
<plugins>
    <plugin>
        <groupId>org.example</groupId>
        <artifactId>flatten-bug-plugin</artifactId>
        <version>${revision}${sha1}-SNAPSHOT</version>
    </plugin>
</plugins>
...
<dependencies>
    <dependency>
        <groupId>org.example</groupId>
        <artifactId>flatten-bug-plugin</artifactId>
        <version>${revision}${sha1}-SNAPSHOT</version>
    </dependency>
</dependencies>
...
```

### Expected result
```
<groupId>org.example</groupId>
<artifactId>flatten-bug-plugin</artifactId>
<version>1.0.0-SNAPSHOT</version>
```

### Actual result
[https://github.com/Azer1652/maven-flatten-bug/blob/main/flatten-bug-child/.flattened-pom.xml](https://github.com/Azer1652/maven-flatten-bug/blob/main/flatten-bug-child/.flattened-pom.xml)
```
<groupId>org.example</groupId>
<artifactId>flatten-bug-plugin</artifactId>
<version>${revision}${sha1}-SNAPSHOT</version>
```
