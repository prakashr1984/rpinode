HDD = ${HDD:-/mnt/usb}
# Build rootfs
.PHONY: build
build:
	@docker build -t prakashr1984/bitcoind . 

.PHONY: init
init:
	@mkdir -p ${HDD}/bitcoin_data
	@cp -f bitcoin.conf ${HDD}/bitcoin_data/bitcoin.conf

.PHONY: run
run:
	@docker run --name bitcoind -d  \
	-v ${HDD}/bitcoin_data:/home/bitcoin/.bitcoin \
	-p 8332:8332 \
	-p 8333:8333 \
	--restart unless-stopped
	prakashr1984/bitcoind 

.PHONY: logs
logs:
	@docker logs -f bitcoind --tail 1000

.PHONY: clean
clean:
	@docker rmi $(docker images -a --filter=dangling=true -q)

