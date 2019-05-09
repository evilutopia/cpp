



boost
---------------------------------------------


boost trac
---------------------------------------------
https://svn.boost.org/trac10/


遇到的bug

+ boost::program_options::error_with_option_name.what() throws std::out_of_range when an empty option is used in the command input
 
  https://svn.boost.org/trac10/ticket/11935


boost tcp acceptor
---------------------------------------------

http://cs.swan.ac.uk/~csoliver/ok-sat-library/internet_html/doc/doc/Boost/1_53_0/doc/html/boost_asio/reference/ip__tcp/acceptor.html

<pre>
boost::asio::ip::tcp::acceptor acceptor(io_service);
boost::asio::ip::tcp::endpoint endpoint(boost::asio::ip::tcp::v4(), port);
acceptor.open(endpoint.protocol());
acceptor.set_option(boost::asio::ip::tcp::acceptor::reuse_address(true));
acceptor.bind(endpoint);
acceptor.listen();
</pre>
