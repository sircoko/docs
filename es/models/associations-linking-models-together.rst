Associations: Linking Models Together
#####################################

Una de las herramientas más poderosas de CakePHP es la capacidad de crear tablas relacionales en el modelo. En CakePHP, los vínculos entre modelos son manejados a través de asociaciones. 

Definir relaciones entre los diferentes objetos de su aplicación debe ser un proceso natural. Por ejemplo: para una base de datos de recetas, una receta puede tener muchas críticas, cada crítica pertenece a un solo autor y un autor puede tener muchas recetas. Definir la manera en la que esas relaciones están enlazadas le permitirá acceder a los datos de una forma intuitiva y poderosa. 

El propósito de esta sección es mostrar como planear, definir y utilizar las asociaciones entre los modelos dentro de CakePHP.

Aunque los datos pueden venir de diferentes fuentes, la manera más común de almacenar los datos en las aplicaciones web es por medio de bases de datos relacionales. Gran parte de lo que esta sección pretende cubrir está pensada bajo esa premisa. 

Para información sobre las asociaciones con los modelos de Plugins, por favor refierase a :ref:`plugin-models`.

Tipos de Relaciones
-------------------

Los cuatro tipos de asociaciones en CakePHP son: hasOne, hasMany, belongsTo y hasAndBelongsToMany (HABTM).

=============== ===================== =======================================
Relación        Tipo de Asociación    Ejemplo
=============== ===================== =======================================
uno a uno       hasOne                Un usuario tiene un perfil.
--------------- --------------------- ---------------------------------------
uno a muchos    hasMany               Un usuario puede tener muchas recetas.
--------------- --------------------- ---------------------------------------
muchos a uno    belongsTo             Muchas recetas pertenecen a un usuario
--------------- --------------------- ---------------------------------------
muchos a muchos hasAndBelongsToMany   Una receta tiene y pertenece a muchos ingredientes.
=============== ===================== =======================================

Para aclarar mejor la manera en la que se definen las asociaciones en los modelos: 
Si la tabla del modelo contiene la clave foránea (otro_modelo_id), este modelo **siempre* va a **pertenecer**(belongTo) a otro modelo. 
Las asociaciones se definen creando una variable de la clase, que tendrá el nombre del tipo de asociación que está definiendo. Esta variable puede ser una simple cadena de caracteres o puede ser un arreglo multidimensional que permita definir asociaciones más específicas.

::

    class Usuario extends AppModel {
        public $hasOne = 'Perfil';
        public $hasMany = array(
            'Receta' => array(
                'className' => 'Receta',
                'conditions' => array('Receta.aprobada' => '1'),
                'order' => 'Receta.created DESC'
            )
        );
    }

.. nota::
    El campo "created" se dejó igual que en la documentación en inglés, ya que forma parte de las convenciones del Framework y CakePHP gestionará este campo de forma automática. 

.. note::
    La documentación no es compatible actualmente con el idioma español en esta página.

    Por favor, siéntase libre de enviarnos un pull request en
    `Github <https://github.com/cakephp/docs>`_ o utilizar el botón **Improve this Doc** para proponer directamente los cambios.

    Usted puede hacer referencia a la versión en Inglés en el menú de selección superior
    para obtener información sobre el tema de esta página.

.. meta::
    :title lang=es: Associations: Linking Models Together
    :keywords lang=es: relationship types,relational mapping,recipe database,relational database,this section covers,web applications,recipes,models,cakephp,storage
