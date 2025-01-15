# Rails juego de garrote venezolano (api).

Este es un proyecto backend principalmente. Y sera la version original de para el backend de la pagina juegodegarrotevenezolano.com

## Base de datos

Consta de los siguientes modelos:

#### Usuario

Modelo para guardar inicios de sesion de los usuarios de la pagina.

```ruby
Users
t.integer "id"                 # clave primaria del modelo
t.string :username            # Nombre de usuario
t.string :email, null: false, unique: true  # Correo electrónico, no puede ser nulo, único
t.string :digest_password     # Contraseña cifrada
t.timestamps                  # Marca de tiempo (created_at y updated_at)


```

#### Admin

Modelo de datos para labores administrativas, pagos, cuentas pendientes, aprobacion de publicaciones,
aprobacion de archivos, moderacion de publicaciones y comentarios.

```ruby
Admins
t.integer "id"                 # clave primaria del modelo
t.string :email, null: false, unique: true  # Correo electrónico, no puede ser nulo, único
t.string :digest_password     # Contraseña cifrada
t.timestamps                  # Marca de tiempo (created_at y updated_at)


```

#### Profile

Guardar data demografica del usuario.

```ruby

Profiles
t.integer "id"                 # clave primaria del modelo
t.string "name"                # Nombre
t.string "lastname"            # Apellido
t.string "address"             # Dirección
t.integer "age"                # Edad
t.string "status"              # Estado
t.string "role"                # Rol
t.integer "years_in_the_game"  # Años en el juego
t.text "biography"             # Biografía
t.string "zipcode"             # Código postal
t.string "phone"               # Teléfono
t.string "email"               # Correo electrónico
t.string "style"               # Estilo
t.references "master", optional: true, foreign_key: { to_table: :users }  # Referencia opcional a un usuario maestro
t.timestamps                   # Marca de tiempo (created_at y updated_at)


```

#### Patios

guardar espacios de entrenamiento de los usuarios que tengan un maestro (un usuario con esa categoria en su profile),
y una direccion fisica.

```ruby

Patios
t.integer :master_id           # ID del maestro
t.integer :id                  # ID del patio
t.integer :name                # Nombre del patio (esto debería ser string en vez de integer)
t.integer :address             # Dirección (esto debería ser string en vez de integer)
t.integer :zip_code            # Código postal (esto debería ser string en vez de integer)
t.integer :contact_phone       # Teléfono de contacto (esto debería ser string en vez de integer)
t.integer :contact_email       # Correo electrónico de contacto (esto debería ser string en vez de integer)
t.timestamps                   # Marca de tiempo (created_at y updated_at)

```

#### Items

Items a la venta relacionados con el juego de garrote venezolano, pertenecientes a usuarios autorizados.

```ruby

Items
t.integer "id"                 # clave primaria del modelo

t.string "item_name"           # Nombre del artículo
t.decimal "price"              # Precio del artículo
t.references "user", foreign_key: true  # Referencia a usuario, clave foránea
t.integer "quantity"           # Cantidad
t.integer "user_id"            # ID del usuario (redundante si ya usas `t.references "user"`)
t.timestamps                   # Marca de tiempo (created_at y updated_at)


```

#### carts

Carritos de compras, por usuario.

```ruby

Carts
t.integer "id"                 # clave primaria del modelo
t.integer "user_id"            # FK del modelo para la relacion "belongs_to"
t.timestamps                   # Marca de tiempo (created_at y updated_at)

```

#### CartItems

Join Table para colocar items en los carritos.

```ruby

CartItems
t.integer "id"                 # clave primaria del modelo
t.integer "item_id"            # ID del artículo
t.integer "cart_id"            # ID del carrito
t.integer "quantity"           # Cantidad
t.timestamps                   # Marca de tiempo (created_at y updated_at), con un pequeño error tipográfico en `timestampts`

```

#### Publications

Escritos, archivos, publicaciones, relacionadas con el juego de garrote.

```ruby

Publications
t.integer "id"                 # clave primaria del modelo

t.integer 'admin_id'            # ID del admin
t.string 'title'               # Título de la publicación
t.string 'review'              # Revisión o contenido de la publicación
t.string 'original_url'        # URL original
t.file 'file'                  # Archivo (esto debería ser manejado con Active Storage o Paperclip)
t.timestamps                   # Marca de tiempo (created_at y updated_at)


```

#### Posts

blog posts de los usuarios.

```ruby
Posts
t.integer "id"                 # clave primaria del modelo

t.integer 'user_id'            # ID del usuario
t.string 'title'               # Título del post
t.string 'text'                # Texto del post
t.timestamps                   # Marca de tiempo (created_at y updated_at)

```

#### Comments

comentarios de los posts de los usuarios.

```ruby

Comments
t.integer "id"                 # clave primaria del modelo

t.integer 'user_id'            # ID del usuario
t.string 'text'                # Texto del comentario
t.timestamps                   # Marca de tiempo (created_at y updated_at)

```
