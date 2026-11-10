obj-$(CONFIG_ZSTD_COMPRESS) += zstd_compress.o
obj-$(CONFIG_ZSTD_DECOMPRESS) += zstd_decompress.o

ccflags-y += -O3

zstd_compress-y := fse_compress.o huf_compress.o compress.o
zstd_decompress-y := huf_decompress.o decompress.o

# Keep the common objects in only one composite object.  LTO links the
# resulting archive with --whole-archive, so embedding them in both the
# compressor and decompressor produces duplicate symbols with LLD.
ifeq ($(CONFIG_ZSTD_COMPRESS),y)
zstd_compress-y += entropy_common.o fse_decompress.o zstd_common.o
else
zstd_decompress-y += entropy_common.o fse_decompress.o zstd_common.o
endif
