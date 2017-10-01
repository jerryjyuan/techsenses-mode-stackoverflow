

#Technical Summries - Grails:

##Notes:

1. Pros:
	Knowledge Bases:	Complete Set of Knowledge Bases
	Concepts:		Gain clear concepts or unknown concepts - and know why + remove confusions and guesses
	Inside-Out:		Know inside-out: good for varied scenarios of usage + new ideas + inventions
	New Versions:	Catch up with newer versions and ever-evolving changes

2. How to reuse "Pure" Technical Contents - without violation of Company Trademarks/Copyrights/Brands/Privacies/Secrets?
	Method 1: Make sure these contents are JUST the research from online resources - technical scenarios - nothing about company contents
			  These contents are indeed open source / online technical resources
	Method 2: Use: github - this might be better
					  Why?
					  	Open source world - use: public repositories - so it belongs to open source world
					  	Copy Paste technical contents- much better than sending emails or files
				 Not Use:
				 	emails to private email addresses
				 	disks
				 	...

3. Core Coupling: 4 Players
		Grails + Groovy + Spring Boot + Gradle
			Grails 3.x - bundled with Gradle
			Grails MVC App + Groovy
			Grails DI + Spring/Spring Boot

4. Grails/Groovy:
		Use templates
		Use commands
		
##App Types:
		
		Type 1: G3: Groovy and Grails MVC + Gradle
					Apache Groovy/Grails/Gradle technologies
					https://g3summit.com/conference/austin/2017/11/home
		Type 2: Groovy and Grails MVC
		Type 3: Standalone
		Type 4: Grails + Spring / Spring Boot
					https://objectcomputing.com/index.php/training/register/offering/110/
		Type 5: Integrations:
				Frontend: UI
				Test Frameworks
				GR8Conf

##IDE:
	Intellij IDEA, Eclipse, Sublime, Textmate
	
##Features:
		1.3.9 / 2.5.6 / 3.3.1 (3.3.0)
	MVC:
		Convention-over-Configuration
	Template-Based and Powered:
		create apps with CLI
	GORM:
		Integrated ORM / NoSQL support
	GSP:
		a powerful view technology
	Plugins:
	Spring:
		Spring-powered dependency injection
		Grails 3 which is built on top of Spring Boot facilitates building Microservices seamlessly
	DSLs
	
##References:

1. APIs + User Guides + Features:
		https://grails.org/documentation.html
		http://docs.grails.org/latest/guide/single.html
		
##Review - Documentation:
	http://docs.grails.org/latest/guide/single.html - 3.3.0

	1) Core:
		GORM / GSP (Groovy Server Pages) + JSON-View / DI / Events / Test Framework
		
	2) Scenarios:
		Installation / Create-App / CLI / Interactive-Mode / IDE / 	Application Development Cycles

	3) Configurations
		environment, system properties and the local application configuration
		(a) Profiles: encapsulate: "commands + features + templates + skeletons + plugins + etc."
				> Unlike scripts, commands cause the Grails environment to start and you have full access to the application context and the runtime.
				USER_HOME/.grails/settings.groovy: repos/credentials+... + Profile Defaults
					grailsCentral { url = "https://repo.grails.org/grails/core" }
				USER_HOME/.m2/settings.xml
				profile.yml
					contains: build.gradle + ...
					dependencies + additional dependencies
			grails create-app myapp --profile=rest-api
			grails create-app myapp --profile=myprofile
			> Customized profile(s)
			> Profile Inheritance: multiple inheritances
			> Publishing Profiles
				gradle publishProfile
					> Grails central repository: Github + Bintray
													- https://github.com/grails-profiles
													- https://bintray.com/
				gradle publish
					> Pubish to internal repo
			> Define Profile-Based Commands:
				> This is powerful - we can define customized commands
				1) YAML
				2) Groovy Script Files
					http://docs.grails.org/3.3.0/api/org/grails/cli/profile/commands/script/GroovyScriptCommand.html
					http://docs.grails.org/latest/guide/commandLine.html#creatingCustomScripts
					grails create-script hello-world:
						> src/main/scripts/hello-world.groovy
				> Groovy Script Powers:
					> Generate commands
					> Copy templates from your plugin or profile
			> Profile Design:
				Parent/Root Profile + Child Profiles
		(b) Configurations Scenarios:
			Config Files: application.yml
				grails-app/conf/application.yml
				Groovy Style:
					grails-app/conf/application.groovy
				Runtime Configuration Access:
					def recipient = grailsApplication.config.getProperty('foo.bar.hello')
					def max = grailsApplication.config.getProperty('foo.bar.max.hellos', Integer, 5)
			        //Retrieve property 'foo.bar.greeting' without specifying type (default is String), otherwise use value "Hello"
			        def greeting = grailsApplication.config.getProperty('foo.bar.greeting', "Hello")
			    Based on: Spring’s PropertySource + Value
			    Runtime settings
		    System properties / command line arguments:
		    	system properties:
		    		systemProperties = System.properties
		    		./gradlew -Dlogging.config=/Users/me/config/logback.groovy bootRun
		    	command line arguments:
		    		url: '${JDBC_CONNECTION_STRING}'
		    	environment:
		    		$ export LOGGING_CONFIG=/Users/me/config/logback.groovy
					$ ./gradlew bootRun
			Logging:
				https://logback.qos.ch/manual/groovy.html		    	
				Logback logging framework: grails-app/conf/logback.groovy (logback.xml)
				Grails artifacts (controllers, services …​) get injected a log property automatically.
				External Configuration File
					logging:
					    config: /Users/me/config/logback.groovy
				./gradlew -Dlogging.config=/Users/me/config/logback.groovy bootRun
		(c) build.gradle:
			1) Dependencies:
				compile 'org.springframework.boot:spring-boot-starter-logging'
				compile('org.springframework.boot:spring-boot-starter-actuator')
				runtime 'org.grails.plugins:asset-pipeline'
				testCompile 'org.grails:grails-plugin-testing'
				testRuntime 'org.seleniumhq.selenium:selenium-htmlunit-driver:2.44.0'
				console 'org.grails:grails-console'
				> dependency management plugin which configures a Maven BOM that defines the default dependency versions 
					for certain "commonly used" dependencies and plugins:
				    imports {
				        mavenBom 'org.grails:grails-bom:' + grailsVersion	> Define common jars' versions inside it
				    }
		(d) Versions:
			def version = grailsApplication.metadata.getApplicationVersion()
			def grailsVersion = grailsApplication.metadata.getGrailsVersion()
			def grailsVersion = GrailsUtil.grailsVersion

	4) Environments
		http://docs.grails.org/latest/guide/single.html#environments
		grails <<environment>>* <<target>> <<arguments>>*'
		grails <<environment>> <<command name>>
		grails war --non-interactive
			Built-in: dev/test/prod: grails test war
			Other:    grails -Dgrails.env=UAT run-app
		Per Environment Bootstrapping
			grails-app/init/BootStrap.groovy
		Generic Per Environment Execution
	5) Applications
		Run App:
			IDE - run
			IDE - run debugger: run-app --debug-jvm
			grails package
				$ java -jar build/libs/myapp-0.1.war
		Customization:
			Customizing Scanning
			Registering Additional Beans
			GrailsApplicationLifeCycle interface
	6) CLI - Interactive Mode
		Grails Commands - Core:
			http://docs.grails.org/latest/ref/Command%20Line/Usage.html
			1) grails create-app myapp
					> a default build.gradle is created
						Plugins Defined:
						1) Gradle + other 3rd party Gradle plugins
						2) Grails Gradle Plugins
			   grails create-app myapp --profile=rest-api
			   grails create-app myapp --profile=myprofile
			   grails create-app myapp --profile mycompany
			   grails create-app myapp --profile com.mycompany:mycompany:1.0.1
			   grails create-app myapp --profile myprofile --features myfeature,hibernate
			   When a profile is used: key - automated and more configured
				   > The build.gradle file is generated is result of obtaining all of the dependency information defined in the profile.yml files and produces the required dependencies.
				   > The command will also merge any build.gradle files defined within a profile and its parent profiles.
			2) gradle install
				publish the profile to your local repository - similar to mvn install
			3) grails create-command HelloWorld
				> grails-app/commands/HelloWorldCommand
		Interactive Mode:
			open
			!
	7) Grails MVC

	8) 

	9) Misc:
		GORM
			http://gorm.grails.org/6.0.x/hibernate/manual/	- TBD
			Hibernate/Method-Chaining/
			grails create-domain-class helloworld.Person
				grails-app/domain/helloworld/Person.groovy
			grails console: Interactive UI
			CRUD: Match underlying Hibernate operations: get()/read():read-only/load():proxy-only
			In-memory database: H2
				http://localhost:8080/dbconsole
				Development: grails.dbconsole.enabled = true
			Data Source + Multiple Data Sources: Domain Classes + Services Classes
				grails-app/conf/hibernate.cfg.xml - default
				grails-app/conf/ds2_hibernate.cfg.xml
				A transactional service can only use a single DataSource, so be sure to only make changes for domain classes whose DataSource is the same as the Service.
			Grails to use the Best Effort 1PC pattern for handling transactions across multiple datasources
		Security
			HTTPS - Proxy:
				Eclipse
				Grails
					grails command can connect and authenticate via a proxy
						The default profile repository is resolved over HTTPS
					1) Unix
						export GRAILS_OPTS="-Dhttps.proxyHost=127.0.0.1 -Dhttps.proxyPort=3128 -Dhttp.proxyUser=test -Dhttp.proxyPassword=test"
						Refer to Java Doc:
							http://docs.oracle.com/javase/7/docs/technotes/guides/net/properties.html
							Networking Properties
							https://git-wip-us.apache.org/repos/asf?p=ant.git;a=blob;f=src/main/org/apache/tools/ant/util/ProxySetup.java;hb=HEAD
					2) Windows
						add environmental variable: GRAILS_OPTS
					Another option is: groovy script file? - also depends upon versions?
						GRADLE_USER_HOME(USER_HOME/.gradle)/ProxySettings.groovy
				Gradle
					https://docs.gradle.org/current/userguide/build_environment.html#sec:accessing_the_web_via_a_proxy
		DI:
			Spring bean, i.e. using dependency injection:
				class MyService {
				   def dataSourceUnproxied
				   ...
				}
				or by pulling it from the ApplicationContext:
					def dataSourceUnproxied = ctx.dataSourceUnproxied
		REST
		i18n
		Testing
			grails -clean test-app
			Targeting Tests
				grails test-app some.org.**.*
				grails test-app some.org.*
				grails test-app some.org.*Controller
				grails test-app *Controller
				grails test-app SimpleController
				grails test-app SimpleController.testLogin
				Combined:
					grails test-app some.org.* SimpleController.testLogin BookController
				Grails 3.x Conventions: *Spec
					grails test-app *.ProductControllerSpec
			Debugging:
				grails --debug-jvm test-app
				> open the default Java remote debugging port, 5005, for you to attach a remote debugger from your editor / IDE of choice
		Plugins
		Integration + Gradle:
			Gradle Tooling APIs:
				https://docs.gradle.org/current/userguide/embedding.html
				Embedding Gradle into your own software: Grails - embedded version of Gradle
					1) Method 1: grails (command/task) -> Gradle (target): mapping
								grails clean 	> 	gradle clean
								grails compile 	> 	gradle classes
								grails package 	> 	gradle assemble
								grails run-app 	> 	gradle bootRun
								grails test-app > 	gradle test
								grails test-app --integration > 	gradle integrationTest
								grails war		> 	gradle assemble
					2) Method 2: gradle <Gradle-version-command-name>
					3) Method 3: use bundled Gradle version:
								 grails gradle command
								 > Interactive Mode: more efficient
								 gradle tasks
				Examples:
				> IDE, CI server, other UI authors; however, the API is open for anyone who needs to embed Gradle in their application.
					Gradle TestKit uses the Tooling API for functional testing of your Gradle plugins.
					Eclipse Buildship uses the Tooling API for importing your Gradle project and running tasks.
					IntelliJ IDEA uses the Tooling API for importing your Gradle project and running tasks.
			Gradle:
				> https://docs.gradle.org/current/userguide/artifact_dependencies_tutorial.html
				> https://docs.gradle.org/current/userguide/dependency_management.html
				> Gradle caches dynamic versions and changing modules for 24 hours. You can override the default cache modes using command line options.
					Fine-tuned control over dependency caching
					Command line options to override caching
						 --offline command line switch tells Gradle to always use dependency modules from the cache
						 To refresh all dependencies in the dependency cache, use the --refresh-dependencies option on the command line.
						 > The --refresh-dependencies option tells Gradle to ignore all cached entries for resolved modules and artifacts. 
						 	A fresh resolve will be performed against all configured repositories, with dynamic versions recalculated, modules refreshed, 
						 	and artifacts downloaded. However, where possible Gradle will check if the previously downloaded artifacts are valid before downloading again. 
						 	This is done by comparing published SHA1 values in the repository with the SHA1 values for existing downloaded artifacts.
				> Artifacts Download:
					Artifact reuse
					> Before downloading an artifact, Gradle tries to determine the checksum of the required artifact 
						by downloading the sha file associated with that artifact. 
						If the checksum can be retrieved, an artifact is not downloaded 
							if an artifact already exists with the same id and checksum. 
						If the checksum cannot be retrieved from the remote server, the artifact will be downloaded (and ignored if it matches an existing artifact).
				> Repos:
					Formats: Maven and Ivy + flatDir (Flat directory repository)
					Access:	 File Systems + HTTP
					Supported repository transport protocols
					Examples:
						Local Maven repository:
							mavenLocal()
						Maven Google repository:
							google() (https://dl.google.com/dl/android/maven2/)
						mavenCentral() (https://repo1.maven.org/maven2)
						Bintray’s JCenter: jcenter()
						maven {
					        url "http://repo.mycompany.com/maven2"
					    }
					    ivy {
					        url "http://repo.mycompany.com/repo"
					    }
					    ivy {
					        // URL can refer to a local directory
					        url "../local-repo"
					    }
				> Dependencies:
					https://docs.gradle.org/current/dsl/org.gradle.api.artifacts.dsl.DependencyHandler.html
						configurationName dependencyNotation1, dependencyNotation2, ...
							Example:
								 compile 'commons-lang:commons-lang:2.6'
								 config1 "org.sample:client:latest.integration"
								 config2 "org.sample:client:latest.release"
						configurationName(dependencyNotation){
					        configStatement1
					        configStatement2
					    }
					    	Example:
					    		compile('org.hibernate:hibernate:3.1') {
					    		}
					Types:
						External module dependency
							In Maven, a module can have one and only one artifact. 
							In Gradle and Ivy, a module can have multiple artifacts. Each artifact can have a different set of dependencies.
						Project dependency
							configurationName project(':someProject')
							configurationName project(path: ':projectA', configuration: 'someOtherConfiguration')
						File dependency:
							Useful: produce files during the task processes
						Client module dependency
							A dependency on an external module, where the artifacts are located in some repository but the module meta-data is specified by the local build. 
							You use this kind of dependency when you want to override the meta-data for the module.
							configurationName module(moduleNotation) {
							    module dependencies
							}
							> declare transitive dependencies directly in the build script
							> The dependencies of a client module can be normal module dependencies or artifact dependencies or another client module.
						Gradle distribution specific dependencies: groovy + gradle api + ...
							apply plugin: 'groovy'
							  //we will use the Groovy version that ships with Gradle:
							  compile localGroovy()
							  //our plugin requires Gradle API interfaces and classes to compile:
							  compile gradleApi()
							  //we will use the Gradle test-kit to test build logic:
							  testCompile gradleTestKit()
							1) Gradle API dependency
								A dependency on the API of the current Gradle version. 
								You use this kind of dependency when you are developing custom Gradle plugins and task types.
							2) Local Groovy dependency
								A dependency on the Groovy version used by the current Gradle version. 
								You use this kind of dependency when you are developing custom Gradle plugins and task types.
					Format:
						artifact repositories:	string notation:
							configurationName "group:name:version:classifier@extension"
								compile 'commons-lang:commons-lang:2.6'
								testCompile 'org.mockito:mockito:1.9.0-rc1'
						map-style notation:
							configurationName group: group, name: name, version: version, classifier: classifier, ext: extension
								compile group: 'com.google.code.guice', name: 'guice', version: '1.0'
						declaring arbitrary files as dependencies
							compile files('hibernate.jar', 'libs/spring.jar')
						putting all jars from 'libs' onto compile classpath
							compile fileTree('libs')
					Configurations:
						Dependencies are grouped into configurations
						> Default configurations:  the default configuration of that module
						> Configurations - introduced by plugins
							Example:
								apply plugin: 'java'
								//so that we can use 'compile', 'testCompile' for dependencies
								> The Java Library plugin configurations
								https://docs.gradle.org/current/userguide/java_library_plugin.html#sec:java_library_configurations_graph
								1) Existing and being deprecated: compile, testCompile, runtime and testRuntime
								2) Current: api / implementation / compileOnly / runtimeOnly + test<...>
								3) Used for: consumers / library itself
						> Advanced:
							Declaring dependency to a specific configuration of the module.
								compile configuration: 'someConf', group: 'org.someOrg', name: 'someModule', version: '1.0'
							Explicit specification of the artifact. See also ModuleDependency.artifact(groovy.lang.Closure).
								compile(group: 'org.myorg', name: 'someLib', version:'1.0') {
								    //explicitly adding the dependency artifact:
								    artifact {
								    }
								}
					Excluding transitive dependencies
				> Configurations:
					1) Enabled by Gradle Plugins: extendable
					2) Customzied Configurations: can be added
					3) Access:	Useful to access configuration data/info/manipulation:
						configurations.compile.each { File file -> println file.name }
					4) Specifying default dependencies for a configuration
				> Practical Guides:
					1) List "compile" jars file names:
						task listJars {
						    doLast {
						        configurations.compile.each { File file -> println file.name }
						        configurations.alllife.dependencies.each { dep -> println dep.name }
						        println()
						        configurations.alllife.allDependencies.each { dep -> println dep.name }
						        println()
						        configurations.alllife.allDependencies.findAll { dep -> dep.name != 'orca' }
						            .each { dep -> println dep.name }
						    }
						}
						gradle -q listJars
				> Dependency/Properties reports
					gradle -q dependencies api:dependencies webapp:dependencies
					gradle -q api:dependencies --configuration testCompile
					gradle buildEnvironment
					gradle -q webapp:dependencyInsight --dependency groovy --configuration compile
					gradle -q api:properties
				> Profiling a build
					--profile command line
					The times for configuration and task execution are sorted with the most expensive operations first.
				> Dry Run
					gradle -m clean compile: you’ll see all the tasks that would be executed as part of the clean and compile tasks
				> Plugins:
					Extensions of Gradle functionalities
					(1) Add Tasks:
						Such as: project report plugin - https://docs.gradle.org/current/userguide/project_reports_plugin.html
					(2) Add Configurations: - define any dependency configurations
						Such as: Java plugin: add configurations: "compile/implementation/runtimeOnly" ...
					(3) Add Conventional Properties
						Add object(s) + APIs access to the object(s):
							https://docs.gradle.org/current/dsl/org.gradle.api.plugins.ProjectReportsPluginConvention.html
					(4) Layouts
				> Tasks:
					gradle [option...] [task...]
					Options:
						https://docs.gradle.org/current/userguide/gradle_command_line.html
						--continue:		Gradle will execute every task to be executed where all of the dependencies for that task completed without failure, instead of stopping as soon as the first failure is encountered. Each of the encountered failures will be reported at the end of the build.
						--rerun-tasks:	Force Gradle to run all the task
					Tasks:
						Gradle CLI tasks + Plugin-added-tasks
						Plugin-added tasks could do the same work + additional work
					Task Groups:
						group = default / build / build setup / help / other
					Task Types: assigned to a group or not
						visible tasks
							gradle -q tasks
						hidden tasks
							gradle -q tasks --all
					Task Types: scope
						root project 'projectReports'
						sub-project
					gradle -q help --task libs
				> Info:
					gradle -q projects
					gradle -q tasks
				> Build environment: gradle.properties: project-root-dir -> gradle-user-home (GRADLE_USER_HOME environment variable, if not set defaults to USER_HOME/.gradle) -> system properties
					https://docs.gradle.org/current/userguide/build_environment.html#sec:accessing_the_web_via_a_proxy
					System properties examples:
						org.gradle.daemon / org.gradle.java.home / org.gradle.jvmargs / org.gradle.logging.level / org.gradle.caching
					Project Properties:
						Environmmental Variables:
							export ORG_GRADLE_PROJECT_prop=somevalue
						System Properties:
							-Dorg.gradle.project.prop=somevalue
						gradle.properties: set up system properties
							systemProp.<prop>=systemValue
						-P
						gradle -q -PcommandLineProjectProp=commandLineProjectPropValue -Dorg.gradle.project.systemProjectProp=systemPropertyValue printProps
					Proxy:
						https://docs.gradle.org/current/userguide/build_environment.html#sec:accessing_the_web_via_a_proxy
						> for downloading dependencies
						gradle.properties:
							systemProp.http(s).proxyHost=www.somehost.org
							systemProp.http(s).proxyPort=8080
							systemProp.http(s).proxyUser=userid
							systemProp.http(s).proxyPassword=password
							systemProp.http(s).nonProxyHosts=*.nonproxyrepos.com|localhost
					Daemon:
						The Gradle Daemon is enabled by default starting with Gradle 3.0, so you don’t have to do anything to benefit from it.
						https://docs.gradle.org/current/userguide/gradle_daemon.html
		Integration + Spring
			http://docs.grails.org/3.3.0/api/grails/boot/config/GrailsAutoConfiguration.html
		CORS
		Traits
		
##Review - User Guides:

##Review - APIs:

##Review - Applications:

##Misc

1. Source Code

2. ...

