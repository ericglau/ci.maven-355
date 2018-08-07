# ci.maven-355
Recreate for WASdev/ci.maven [issue 355](https://github.com/WASdev/ci.maven/issues/355)

## Recreate of NPE in issue 355

1. Run 
```bash
$ mvn package # this will fail with error mentioned below
```

2. Install features manually into the target WLP install
```bash
$ cd target/liberty/wlp/
$ ./bin/installUtility install wsSecuritySaml-1.1  --acceptLicense 
$ ./bin/installUtility install jaxrs-2.0  --acceptLicense 
```

3. Run package once (this works)
```bash
$ mvn package  # (or 'pre-package')
```

4. Run package a second time (this fails).
```bash
$ mvn package 
```
with error:
```bash
[ERROR] Failed to execute goal net.wasdev.wlp.maven.plugins:liberty-maven-plugin:2.5:install-feature (create-server) on project test_355: null: MojoExecutionException: NullPointerException -> [Help 1]
```

## Other issue?

IF I skip running the installUtility and just do:

```bash
mvn package  # (or mvn prepare-package)
```

This results in:
```bash
[ERROR] Failed to execute goal net.wasdev.wlp.maven.plugins:liberty-maven-plugin:2.5:install-feature (create-server) on project test_355: com.ibm.ws.install.InstallException: CWWKF1385E: The [javaee-8.0, localconnector-1.0, microprofile-1.3, wsSecuritySaml-1.1] assets depend on com.ibm.websphere.appserver.javaeeCompatible-6.0, which is not available in the IBM WebSphere Liberty Repository. If the required asset is a feature that you previously downloaded, install the missing feature by specifying the location of the feature ESA file on the featureManager install --location option, and try to install [javaee-8.0, localconnector-1.0, microprofile-1.3, wsSecuritySaml-1.1] again. -> [Help 1]
```


