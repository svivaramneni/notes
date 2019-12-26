### Challenges without Spring Boot
* Any time spent in writing configuration is time spent not writing application logic. 
* Managing project dependencies with versions is tricky. Especially the transitive ones.

### Core Features
* **Automation Configuration**: Spring boot can automatically provide configuration for common application functionality.
* **Starter Dependencies**: If we tell spring boot what functionality is needed, it will ensure corresponding libraries are added to thebuild
* **The Actuator**: It gives insights into whats happening under the covers.

### Conditional Annotations in Spring Boot
* Spring Boot has a very cool set of conditional annotations. Conditional annotations are based upon Spring's Condition interface.
* Conditional configuration allows for configuration to be available in an application, but to be ignored unless certain conditions are met.

`@ConditionalOnClass({ DataSource.class, EmbeddedDatabaseType.class })`


#### Examples: 
* If SpringBoot detects JdbcTemplate in the classpath, then it will automatically configure jdbcTemplate bean. This way boiler plate code could be avoided.
* If SpringMVC is on the classpath, Spring’s DispatcherServlet will be configured and SpringMVC enabled.

### SpringBootApplication Annotation
It combines 3 useful annotations
* **@Configuration**: Designates a class as a configuration class.
* **@ComponentScan**: Enables component scanning. So that, our web controllers and other components could be auto discovered and registered as beans in spring application context.
* **@EnableAutoconfiguration**: Enables spring boots magic of auto-configuration.

### Testing Spring Boot Applications
The use of @SpringApplicationConfiguration is largely identical to @ContextConfiguration, with few additional capabilities such as spring boot logging, loading external properties, etc.

`@RunWith(SpringJUnit4ClassRunner.class)
@SpringApplicationConfiguration(
      classes=AddressBookConfiguration.class)
public class AddressServiceTests {
  ...
}
`

### Actuator
* You could get a bean wiring report with “/beans” endpoint. It contains following information.
    * Bean : name/id
    * Dependency beans
    * Resource url to the class file
    * Scope: singleton vs prototype
    * Type: beans java type
* You could get the state of all evaluated conditions with “/autoconfig” endpoint.
* You could get all environment configs with “/env” endpoint.
* “/health”, “/metrics”, “shutdown”


