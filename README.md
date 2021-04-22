name: GHA-frac-Release

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-18.04
    steps:
    - name: Install gtest manually
      run: sudo apt-get install libgtest-dev && cd /usr/src/gtest && sudo cmake CMakeLists.txt && sudo make && sudo cp *.a /usr/lib && sudo ln -s /usr/lib/libgtest.a /usr/local/lib/libgtest.a && sudo ln -s /usr/lib/libgtest_main.a /usr/local/lib/libgtest_main.a
    - uses: actions/checkout@v1
    - name: configure
      run: mkdir build && cd build && cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_CXX_FLAGS="-Werror" ..
    - name: make
      run: cd build && make
    - name: Run Test
      run: /home/runner/work/mod-lab00-training/mod-lab00-training/build/test/mod-lab00-training.test
