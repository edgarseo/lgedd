
# A PARTIR DEL ARCHIVO XML “EJERCICIO1.XML” PROPORCIONADO EN LA CARPETA “FUENTES.ZIP”, CREA UN ARCHIVO XSD (XML SCHEMA) QUE DEFINA LA ESTRUCTURA Y RESTRICCIONES DEL DOCUMENTO XML. A CONTINUACIÓN, VALIDA EL ARCHIVO XML UTILIZANDO EL XSD PARA ASEGURARTE DE QUE CUMPLE CON LAS REGLAS ESPECIFICADAS EN EL PROPIO XML.


```html


<libreria>

	<libro>
	
		<titulo>El Gran Gatsby</titulo>
		
		<autor>F. Scott Fitzgerald</autor>
		
		<anio>1925</anio>
		
		<genero>Ficción</genero>
	
	</libro>
	
	<libro>
	
		<titulo>1984</titulo>
		
		<autor>George Orwell</autor>
		
		<anio>1949</anio>
		
		<genero>Distopía</genero>
	
	</libro>

</libreria>
```


# Solución 

```xml

<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://w3.org">

  <!-- Elemento Raíz -->
  <xs:element name="libreria">
    <xs:complexType>
      <xs:sequence>
        <!-- Elemento Libro (puede repetirse indefinidamente) -->
        <xs:element name="libro" maxOccurs="unbounded" minOccurs="1">
          <xs:complexType>
            <xs:sequence>
              <xs:element name="titulo" type="xs:string"/>
              <xs:element name="autor" type="xs:string"/>
              <xs:element name="anio" type="xs:integer"/>
              <xs:element name="genero" type="xs:string"/>
            </xs:sequence>
          </xs:complexType>
        </xs:element>
      </xs:sequence>
    </xs:complexType>
  </xs:element>

</xs:schema>

```



# A PARTIR DEL ARCHIVO XML “EJERCICIO2.XML” PROPORCIONADO EN LA CARPETA “FUENTES.ZIP”, QUE CONTIENE INFORMACIÓN SOBRE ESTUDIANTES DE UNA UNIVERSIDAD, CREA UN ARCHIVO XSD (XML SCHEMA) QUE DEFINA LA ESTRUCTURA Y LAS RESTRICCIONES DEL DOCUMENTO XML. A CONTINUACIÓN, VALIDA EL ARCHIVO XML UTILIZANDO EL XSD PARA ASEGURARTE DE QUE CUMPLE CON LAS REGLAS ESPECIFICADAS EN EL PROPIO XML.


```xml
<universidad>

	<estudiante>
	
		<nombre>Juan Pérez</nombre>
		
		<edad>20</edad>
		
		<carrera>Ingeniería Informática</carrera>
		
	</estudiante>
	
		<estudiante>
		
		<nombre>María López</nombre>
		
		<edad>22</edad>
	
	<carrera>Arquitectura</carrera>
	
	</estudiante>

</universidad>
```



# Solución


```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://w3.org" elementFormDefault="qualified">

    <!-- ========================================================================= -->
    <!-- Definición de restricciones y tipos simples                               -->
    <!-- ========================================================================= -->
    <xs:simpleType name="tipoEdad">
        <xs:restriction base="xs:integer">
            <xs:minInclusive value="16"/>
            <xs:maxInclusive value="100"/>
        </xs:restriction>
    </xs:simpleType>


    <!-- ========================================================================= -->
    <!-- Estructuras de tipos complejos                                            -->
    <!-- ========================================================================= -->
    <xs:complexType name="tipoEstudiante">
        <xs:sequence>
            <xs:element name="nombre" type="xs:string"/>
            <xs:element name="edad" type="tipoEdad"/>
            <xs:element name="carrera" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>


    <!-- ========================================================================= -->
    <!-- Elemento Raíz                                                             -->
    <!-- ========================================================================= -->
    <xs:element name="universidad">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="estudiante" type="tipoEstudiante" maxOccurs="unbounded"/>
            </xs:sequence>
        </xs:complexType>
    </xs:element>

</xs:schema>


```



# Solución vinculado 

xsd

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://w3.org">

  <!-- Elemento Raíz -->
  <xs:element name="universidad">
    <xs:complexType>
      <xs:sequence>
        <!-- Elemento Estudiante (puede repetirse de forma ilimitada) -->
        <xs:element name="estudiante" maxOccurs="unbounded" minOccurs="1">
          <xs:complexType>
            <xs:sequence>
              <xs:element name="nombre" type="xs:string"/>
              <xs:element name="edad" type="xs:integer"/>
              <xs:element name="carrera" type="xs:string"/>
            </xs:sequence>
          </xs:complexType>
        </xs:element>
      </xs:sequence>
    </xs:complexType>
  </xs:element>

</xs:schema>


```


xml vinculado 


```xml
<?xml version="1.0" encoding="UTF-8"?>
<universidad xmlns:xsi="http://w3.org"
             xsi:noNamespaceSchemaLocation="ejercicio2.xsd">
  <estudiante>
    <nombre>Juan Pérez</nombre>
    <edad>20</edad>
    <carrera>Ingeniería Informática</carrera>
  </estudiante>
  <estudiante>
    <nombre>María López</nombre>
    <edad>22</edad>
    <carrera>Arquitectura</carrera>
  </estudiante>
</universidad>
```




# A PARTIR DEL ARCHIVO XML “EJERCICIO3.XML” PROPORCIONADO EN LA CARPETA “FUENTES.ZIP”, QUE CONTIENE INFORMACIÓN SOBRE PRODUCTOS DE UNA TIENDA EN LÍNEA, CREA UN ARCHIVO XSD (XML SCHEMA) QUE DEFINA LA ESTRUCTURA Y LAS RESTRICCIONES DEL DOCUMENTO XML. A CONTINUACIÓN, VALIDA EL ARCHIVO XML UTILIZANDO EL XSD PARA ASEGURARTE DE QUE CUMPLE CON LAS REGLAS ESPECIFICADAS EN EL PROPIO XML.



```xml
<tienda>

	<producto>
	
		<nombre>Teléfono móvil</nombre>
		
		<precio>299.99</precio>
		
		<cantidad>10</cantidad>
	
	</producto>
	
	<producto>
	
		<nombre>Ordenador portátil</nombre>
		
		<precio>899.99</precio>
		
		<cantidad>5</cantidad>
	
	</producto>

</tienda>

```



# Solución

xsd

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://w3.org" elementFormDefault="qualified">

    <!-- ========================================================================= -->
    <!-- Definición de restricciones y tipos simples                               -->
    <!-- ========================================================================= -->
    <xs:simpleType name="tipoPrecio">
        <xs:restriction base="xs:decimal">
            <xs:minInclusive value="0.00"/>
        </xs:restriction>
    </xs:simpleType>

    <xs:simpleType name="tipoCantidad">
        <xs:restriction base="xs:integer">
            <xs:minInclusive value="0"/>
        </xs:restriction>
    </xs:simpleType>

    <!-- ========================================================================= -->
    <!-- Estructuras de tipos complejos                                            -->
    <!-- ========================================================================= -->
    <xs:complexType name="tipoProducto">
        <xs:sequence>
            <xs:element name="nombre" type="xs:string"/>
            <xs:element name="precio" type="tipoPrecio"/>
            <xs:element name="cantidad" type="tipoCantidad"/>
        </xs:sequence>
    </xs:complexType>

    <!-- ========================================================================= -->
    <!-- Elemento Raíz                                                             -->
    <!-- ========================================================================= -->
    <xs:element name="tienda">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="producto" type="tipoProducto" maxOccurs="unbounded"/>
            </xs:sequence>
        </xs:complexType>
    </xs:element>

</xs:schema>
```


xml vinculado

```xml
<?xml version="1.0" encoding="UTF-8"?>
<tienda xmlns:xsi="http://w3.org"
        xsi:noNamespaceSchemaLocation="ejercicio3.xsd">
    <producto>
        <nombre>Teléfono móvil</nombre>
        <precio>299.99</precio>
        <cantidad>10</cantidad>
    </producto>
    <producto>
        <nombre>Ordenador portátil</nombre>
        <precio>899.99</precio>
        <cantidad>5</cantidad>
    </producto>
</tienda>

```


# A PARTIR DEL ARCHIVO XML “EJERCICIO4.XML” PROPORCIONADO EN LA CARPETA “FUENTES.ZIP”, QUE CONTIENE INFORMACIÓN SOBRE EMPLEADOS DE UNA EMPRESA, CREA UN ARCHIVO XSD (XML SCHEMA) QUE DEFINA LA ESTRUCTURA Y LAS RESTRICCIONES DEL DOCUMENTO XML. A CONTINUACIÓN, VALIDA EL ARCHIVO XML UTILIZANDO EL XSD PARA ASEGURARTE DE QUE CUMPLE CON LAS REGLAS ESPECIFICADAS EN EL PROPIO XML.


```xml
<empresa>

	<empleado id="1">
	
		<nombre>John</nombre>
		
		<apellido>Doe</apellido>
		
		<fechaNacimiento>1990-05-15</fechaNacimiento>
		
		<salario>50000.00</salario>
		
		<activo>true</activo>
		
		<horaEntrada>09:00:00</horaEntrada>
	
	</empleado>
	
		<empleado id="2">
		
		<nombre>Jane</nombre>
		
		<apellido>Smith</apellido>
		
		<fechaNacimiento>1985-08-20</fechaNacimiento>
		
		<salario>60000.50</salario>
		
		<activo>false</activo>
		
		<horaEntrada>08:30:00</horaEntrada>
	
	</empleado>

</empresa>
```


# Solución

xsd

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://w3.org" elementFormDefault="qualified">

    <!-- ========================================================================= -->
    <!-- Definición de restricciones y tipos simples                               -->
    <!-- ========================================================================= -->
    <xs:simpleType name="tipoSalario">
        <xs:restriction base="xs:decimal">
            <xs:minInclusive value="0.00"/>
        </xs:restriction>
    </xs:simpleType>

    <!-- ========================================================================= -->
    <!-- Estructuras de tipos complejos                                            -->
    <!-- ========================================================================= -->
    <xs:complexType name="tipoEmpleado">
        <xs:sequence>
            <xs:element name="nombre" type="xs:string"/>
            <xs:element name="apellido" type="xs:string"/>
            <xs:element name="fechaNacimiento" type="xs:date"/>
            <xs:element name="salario" type="tipoSalario"/>
            <xs:element name="activo" type="xs:boolean"/>
            <xs:element name="horaEntrada" type="xs:time"/>
        </xs:sequence>
        <!-- Declaración del atributo identificador -->
        <xs:attribute name="id" type="xs:positiveInteger" use="required"/>
    </xs:complexType>

    <!-- ========================================================================= -->
    <!-- Elemento Raíz                                                             -->
    <!-- ========================================================================= -->
    <xs:element name="empresa">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="empleado" type="tipoEmpleado" maxOccurs="unbounded"/>
            </xs:sequence>
        </xs:complexType>
    </xs:element>

</xs:schema>

```


xml vinculado 

```xml

<?xml version="1.0" encoding="UTF-8"?>
<empresa xmlns:xsi="http://w3.org"
         xsi:noNamespaceSchemaLocation="ejercicio4.xsd">
    <empleado id="1">
        <nombre>John</nombre>
        <apellido>Doe</apellido>
        <fechaNacimiento>1990-05-15</fechaNacimiento>
        <salario>50000.00</salario>
        <activo>true</activo>
        <horaEntrada>09:00:00</horaEntrada>
    </empleado>
    <empleado id="2">
        <nombre>Jane</nombre>
        <apellido>Smith</apellido>
        <fechaNacimiento>1985-08-20</fechaNacimiento>
        <salario>60000.50</salario>
        <activo>false</activo>
        <horaEntrada>08:30:00</horaEntrada>
    </empleado>
</empresa>

```

