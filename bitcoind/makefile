# Build rootfs
.PHONY: build
build:
	@docker build -t prakashr1984/bitcoind . 

.PHONY: init
init:
	@mkdir -p /mnt/usb/bitcoin_data
	@cp -f bitcoin.conf /mnt/usb/bitcoin_data/bitcoin.conf
	@chmod -R 777 /mnt/usb/bitcoin_data

.PHONY: run
run:
	@docker rm bitcoind || true
	@docker run --name bitcoind -d  \
	-v /mnt/usb/bitcoin_data:/home/bitcoin/.bitcoin \
	-p 8332:8332 \
	-p 8333:8333 \
	--restart unless-stopped \
	prakashr1984/bitcoind 

.PHONY: logs
logs:
	@docker logs -f bitcoind --tail 1000

.PHONY: clean
clean:
	@docker rmi $(docker images -a --filter=dangling=true -q)

