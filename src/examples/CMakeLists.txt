include(CheckLibraryExists)

cmake_minimum_required(VERSION 2.8.9)
project (mpsse_examples)

### Testapp
add_executable(spiflash spiflash.c)
target_link_libraries(spiflash mpsse)
install(TARGETS spiflash RUNTIME DESTINATION bin)
