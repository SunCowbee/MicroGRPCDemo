MicroGRPCDemo:

ENVIRONMENT REQUIRED:

#ubuntu

#go

#protoBuf

protoc --go_out=./ *.proto #不加grpc插件

protoc --go_out=plugins=grpc:./ *.proto #添加grpc插件

#grpc

#consul

consul agent -dev

http://localhost:8500

consul agent -server -bootstrap-expect 2 -data-dir /tmp/consul -node=n1 - bind=192.168.150.20 -ui -config-dir /etc/consul.d -rejoin -join 192.168.150.20 - client 0.0.0.0

consul agent -server -bootstrap-expect 2 -data-dir /tmp/consul -node=n2 - bind=192.168.150.21 -ui -rejoin -join 192.168.150.20

consul agent -data-dir /tmp/consul -node=n3 -bind=192.168.150.23 -config-dir /etc/consul.d -rejoin -join 192.168.150.20

#micro

micro new --type "srv" micro/rpc/srv

micro new --type "web" micro/rpc/web

protoc --proto_path=. --go_out=. --micro_out=. proto/example/example.proto
