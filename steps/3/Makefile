TEST?=./...

include ./make/config.mk

install:
	@if [ ! -d pact/bin ]; then\
		echo "--- 🛠 Installing Pact CLI dependencies";\
		curl -fsSL https://raw.githubusercontent.com/pact-foundation/pact-ruby-standalone/master/install.sh | bash;\
    fi

run-consumer:
	@go run consumer/client/cmd/main.go

run-provider:
	@go run provider/cmd/usersvc/main.go

unit:
	@echo "--- 🔨Running Unit tests "
	go test -tags=unit -count=1 github.com/pact-foundation/pact-workshop-go/consumer/client -run 'TestClientUnit'

consumer: install
	@echo "--- 🔨Running Consumer Pact tests "
	go test -tags=integration -count=1 github.com/pact-foundation/pact-workshop-go/consumer/client -run 'TestClientPact'

.PHONY: install unit consumer provider run-provider run-consumer
