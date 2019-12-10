
## ssl short read

在ssl 中经常会出现ssl short read,查了一下资料主要原因为关闭也需要close_notify机制。
遇到该类问题大致可以认为对端要关闭ssl连接，但是没有按照ssl关闭的close_notify机制来关闭。

https://stackoverflow.com/questions/25587403/boost-asio-ssl-async-shutdown-always-finishes-with-an-error
