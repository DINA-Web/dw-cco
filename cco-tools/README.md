Important files
===============

These files are important for building the cco-tools image:

    * Dockerfile
    * cco_poc
    * pom.xml
    * liquibase.properties
      - liquibase.properties.mysql
      - liquibase.properties.postgres

The `Dockerfile` defines a custom image `cco-tools`, which builds in a clean environment using the latest official Maven image from Docker Hub. The default command is `mvn clean install` (which can be overridden).

The `cco_poc` comes from the GitHub repo for the Complex Collections Objects data model, which is copied into the container image during the build step. The script `get_cco.sh` can be used to do this the first time.

The other files in the list above are needed, because of a couple of modifications to the GitHub code:

    * pom.xml
    * liquibase.properties - files

The modified pom.xml was required because the maven build failed with an X11 error (despite this being a headless build, perhaps a maven or Oracle JDK bug?), this was resolved by adding:

    <promptOnNonLocalDatabase>false</promptOnNonLocalDatabase>

The liquibase.properties file is a copy of either the `.mysql` or the `.postgres` properties files and contains credentials matching those of other running Docker containers so no configuration would be required other than starting the composite Docker application `dw-cco`.
