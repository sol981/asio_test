
# How to use

## This demo can run with local host or 2 device have connection through internet 
* server.cpp
  - read message from client and write message to client
* clent.cpp
  - read message from server and write data to server
* ioservice1
  - test async_wait with multil thread
  
## Build:
    g++ server.cpp -o server -lpthread
    g++ client.cpp -o client -lpthread
    g++ thread.cpp -o thread -lpthread

## Run:
    ./server
    open other terminal
    ./client

# Explain

## Client
	tcp::resolver::query q{"127.0.0.1", "2014"};
	resolv.async_resolve(q, resolve_handler);
	ioservice.run();

## Handler 
  * resolve_handler: call asyn_connect()
  * connect handler: call async_read(), async_write(), write()
  * read_handler: cout.write <<

## Variables:
  * io_service ioservice;
  * tcp::resolver resolv{ioservice};
  * tcp::socket tcp_socket{ioservice};

## Server
  * tcp_acceptor.listen();
  * tcp_acceptor.async_accept(tcp_socket, accept_handler);
  * ioservice.run();

## Handler 
  * accept_handler:  call async_read(), async_write()
  * read_handler: cout.write <<

## Variables:
  * io_service ioservice;
  * tcp::endpoint tcp_endpoint{tcp::v4(), 2014};
  * tcp::acceptor tcp_acceptor{ioservice, tcp_endpoint};
  * tcp::socket tcp_socket{ioservice};

## link 
https://theboostcpplibraries.com/boost.asio-network-programming