# Version del esquema de configuracion de CircleCI que usa este archivo
version: 2.1

# Aqui se definen los jobs, es decir, las tareas que CircleCI puede ejecutar
jobs:
  # Job llamado "saludo"
  saludo:
    # Este job correra dentro de un contenedor Docker
    docker:
      # Imagen base que CircleCI levantara para ejecutar los pasos
      - image: cimg/base:stable
    # Lista de pasos que ejecuta el job
    steps:
      # Ejecuta un comando en la terminal e imprime un saludo en los logs
      - run : echo "Hola, este es un saludo desde CircleCI"

  # Segundo job llamado "despidete"
  despidete:
    # Igual que el job anterior, usa un contenedor Docker
    docker:
      # Imagen del contenedor donde se ejecutaran los comandos
      - image: cimg/base:stable
    # Pasos del job
    steps:
      # Primer mensaje de despedida
      - run : echo "chao 1"
      # Segundo mensaje de despedida
      - run : echo "chao 2"
      # Tercer mensaje de despedida
      - run : echo "chao 3"


# Aqui se definen los workflows, o sea, la forma en que se organizan y ejecutan los jobs
workflows:
  # Primer workflow: ejecuta los dos jobs
  workflows1:
    jobs:
      # Ejecuta el job "saludo"
      - saludo
      # Ejecuta el job "despidete"
      - despidete
  # Segundo workflow: tambien usa los dos jobs, pero con dependencia entre ellos
  workflows2:
    jobs:
      # Primero se ejecuta "saludo"
      - saludo
      # "despidete" solo corre cuando "saludo" termina correctamente
      - despidete:
          requires:
            # Indica que este job depende del job "saludo"
            - saludo
