Boost C++11 Server Example
============================

This example shows how to customise the allocation of memory associated with asynchronous operations.

Link:

[Original server.cpp example](http://www.boost.org/doc/libs/1_55_0/doc/html/boost_asio/example/cpp11/allocation/server.cpp)


Example
---------
First, create a new project with a block:

	~$bii init boost_server
	~/boost_server$cd boost_server
	~/boost_server$bii new myuser/boost_block

Here is the code you can copy&paste to any project block, in this case to *~/boost\_server/myuser/boost\_block/* directory

**main.cpp**

	#include <phil/boost_example/server.h>
	#include <iostream>

	int main(int argc, char* argv[]) {
	  try {
	    if (argc != 2) {
	      std::cerr << "Usage: server <port>\n";
	      return 1;
	    }
	    boost::asio::io_service io_service;
	    server s(io_service, std::atoi(argv[1]));
	    io_service.run();
	  } catch (std::exception& e) {
	    std::cerr << "Exception: " << e.what() << "\n";
	  }
	  return 0;
	}