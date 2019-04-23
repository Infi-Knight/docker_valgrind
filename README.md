# docker_valgrind

- Valgrind isn't supported on macOS mojave yet, so we can use docker to run valgrind.
- Reference: [https://www.gungorbudak.com/blog/2018/06/13/memory-leak-testing-with-valgrind-on-macos-using-docker-containers/](https://www.gungorbudak.com/blog/2018/06/13/memory-leak-testing-with-valgrind-on-macos-using-docker-containers/)
- build the docker image using provided `DOCKERFILE`:
  `docker build -t memory-test:0.1 .`
- Sample run for a simple c++ program:
  `docker run -ti -v $PWD:/test memory-test:0.1 bash -c "cd /test/; g++ -o main.out main.cpp && valgrind --leak-check=full ./main.out"`
- Commands:
  - `docker run -ti`: interactively run docker image
  - `-v $PWD:/test`  is the option for mounting current working directory (where we have the code and Dockerfile) under /test/ directory within the executed container. In this way, you can keep modifying code outside the container and still test the its most up-to-date version.
  - `memory-test:0.1`: name of the docker image
  - `bash -c "cd /test/; g++ -o main.out main.cpp && valgrind --leak-check=full ./main.out" `:  to change directory, build the C++ code and finally do memory leak check with Valgrind on the executable
