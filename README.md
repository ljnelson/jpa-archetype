# jpa-archetype

This is (going to be) a Maven archetype for building JPA entities that
are capable of being tested against the Big Three JPA providers
([Hibernate][1], [EclipseLink][2] and [OpenJPA][3]).

The root `pom.xml` is fairly enormous.  :-) Most of what it does is
copy various files into isolated areas where they can be bytecode
enhanced at build time by the providers' individual non-standard
mechanisms.

It is necessary in such cases to make sure that dependencies on the
classpath that are needed for integration testing---that might of
course contain other entities---are also enhanced.  This accounts for
the vast bulk of the `pom.xml` stanzas.

Four jars are produced at the end of a typical Maven run using this
`pom.xml`.  The first is a normal `.jar` file.  The other three are
enhanced versions of the normal `.jar` file so that if you like you do
not have to further enhance your classes again.

The [Maven Surefire plugin][4] is run three times as part of normal
testing: once per JPA provider, with the other JPA providers'
dependencies weeded out of its classpath.

Questions and feedback heartily welcomed at `ljnelson` at a big
enormous supposedly non-evil email provider starting with G.

[1]: http://hibernate.org
[2]: http://www.eclipse.org/eclipselink/jpa.php
[3]: http://openjpa.apache.org
[4]: http://maven.apache.org/plugins/maven-surefire-plugin/