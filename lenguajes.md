# Lenguajes

## Técnicas

 - Anónimos y cierres: Java lambdas, Ruby procs y blocks, Scala
 - Mixins:
 	- [Ruby modules](http://ruby-doc.com/docs/ProgrammingRuby/html/tut_modules.html)
 		- Ejemplo: [Comparable](https://en.wikipedia.org/wiki/Mixin#In_Ruby)
 	- [Scala traits](http://docs.scala-lang.org/tutorials/tour/traits)
	 	- Ejemplo: [Traits exercise](https://www.scala-exercises.org/std_lib/traits)
 - Reflexión
 - Metaprogramación

## Paradigmas
 - Objetos
 - Eventos
 - Funcional


## Ejercicios

1. Interfaces funcionales - [Formateo de informes](#informes)
2. [Ruby from other languages](https://www.ruby-lang.org/en/documentation/ruby-from-other-languages/)
3. [Scala tour](http://docs.scala-lang.org/tutorials/tour/tour-of-scala)
4. [Scala exercises](https://www.scala-exercises.org/std_lib/)


# Ejercicio 1 - Interfaces funcionales
<a id="informes"></a>
## Formateo de informes

### Versión en ruby

```ruby
class Report
  attr_reader :title, :text
  attr_accessor :formatter
  def initialize(formatter)
    @title = 'Informe mensual'
    @text = ['Todo marcha', 'muy bien.']
    @formatter = formatter
  end
  def output_report()
    @formatter.output_report(self)
  end
end
class HTMLFormatter
  def output_report(context)
    puts('<html>')
    puts(' <head>')
    # Output The rest of the report ...
    puts(" <title>#{context.title}</title>")
    puts(' </head>')
    puts(' <body>')
    context.text.each do |line|
      puts(" <p>#{line}</p>")
    end
    puts(' </body>')
    puts('</html>')
  end
end
	
class PlainTextFormatter
  def output_report(context)
    puts("***** #{context.title} *****")
    context.text.each do |line|
```

#### Procs
- Proc = objeto función = objeto que solo contiene un trozo de código 
 
```ruby
hello = lambda do
```

#### Blocks

- Code block = Función anónima, cierre o lambda
- Es la parte `do` ... `end`
- Simplificada como  `{` ... `}`

```ruby
hello = lambda {
```

- Parametrizable

```ruby
multiply = lambda {|x, y| x * y}

n = multiply.call(20, 3)
```

#### Llamada 

```ruby
name = 'John'
```


#### Paso de bloques como parámetros

- Simplemente, se añade al final de la llamada a un método 
- ¿Dónde se llama al bloque? Donde el método indique con `yield`
- El bloque (realmente un objeto `Proc`) se pasa como una especie de parámetro invisible
 
```ruby
def run_it
```
```ruby
run_it do
```
Salida:

```
Before the yield
```

- Llamada a un bloque con parámetros:

```ruby
def run_it_with_parameter
```
Salida:

```
Before the yield
```

- Hacer explícito el bloque pasado como parámetro: _ampersand_

```ruby
def run_it_with_parameter(&block)
```
Y para convertir un `Proc` en un bloque pasado como parámetro:

```ruby
my_proc = lambda {|x| puts("The value of x is #{x}")}
```

### Versión con interfaces funcionales (Ruby procs + blocks)

```ruby
class Report
	
	
```

Formateo HTML:

```ruby
HTML_FORMATTER = lambda do |context|

report = Report.new &HTML_FORMATTER
```

Formateo de texto:

```ruby
report = Report.new do |context|
```