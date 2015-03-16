To avoid the ViewExpiredException generated for a JSF expired session and directly generate a new one, you can use the property
_com.sun.faces.enableRestoreView11Compatibility_ in the web.xml file as follows:

```xml
<context-param> 
	<param-name>com.sun.faces.enableRestoreView11Compatibility</param-name>
	<param-value>true</param-value> 
</context-param>
```