# maven-flatten-bug
### Mini repo to reproduce bug in maven-flatten-plugin

When using `${revision}` or `${sha1}` in `<pluginManagement>` and `<flattenMode>resolveCiFriendliesOnly</flattenMode>`. They do not get replaced.

### Maven config
```
    <properties>
        <sha1/>
        <revision>1.0.0</revision>
    </properties>
```
```
    <build>
        <pluginManagement>
            <plugins>
                <plugin>
                    <groupId>org.example</groupId>
                    <artifactId>flatten-bug-plugin</artifactId>
                    <version>${revision}${sha1}-SNAPSHOT</version>
                </plugin>
            </plugins>
        </pluginManagement>
    </build>
```

### Expected result
```
<build>
        <pluginManagement>
            <plugins>
                <plugin>
                    <groupId>org.example</groupId>
                    <artifactId>flatten-bug-plugin</artifactId>
                    <version>1.0.0-SNAPSHOT</version>
                </plugin>
            </plugins>
        </pluginManagement>
    </build>
```

### Actual result
```
  <build>
    <pluginManagement>
      <plugins>
        <plugin>
          <groupId>org.example</groupId>
          <artifactId>flatten-bug-plugin</artifactId>
          <version>${revision}${sha1}-SNAPSHOT</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
```
