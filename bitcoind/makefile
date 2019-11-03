# Build rootfs
.PHONY: build
build:
	@docker build -t prakashr1984/bitcoind . 

.PHONY: init
init:
	@mkdir -p /mnt/usb/bitcoin_data
	@cp -f bitcoin.conf /mnt/usb/bitcoin_data/bitcoin.conf
	@chmod -R 777 /mnt/usb/bitcoin_data

.PHONY: updateconf
updateconf:
	@cp -f bitcoin.conf /mnt/usb/bitcoin_data/bitcoin.conf


.PHONY: stop
stop: remove
	@docker stop bitcoind || true

.PHONY: remove
remove: stop
	@docker rm bitcoind || true

.PHONY: run
run: stop
	@docker run --name bitcoind -d  \
	-v /mnt/usb/bitcoin_data:/home/bitcoin/.bitcoin \
	-p 8332:8332 \
	-p 8333:8333 \
	--restart unless-stopped \
	prakashr1984/bitcoind 


.PHONY: logs
logs:
	@docker logs -f bitcoind --tail 1000

.PHONY: rmi
rmi:
	@docker rmi -f $(shell docker images -a --filter=dangling=true -q) || true

.PHONY: rm
rm:
	@docker rm $(shell docker ps -a -f status=exited -q) || true

.PHONY: clean
clean: rmi rm
	@echo "cleanup done!!"
