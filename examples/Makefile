
-include ../Makefile.config

EXAMPLES_$(ENABLE_AVRO_CPP) += serdes-tool
EXAMPLES_$(ENABLE_AVRO_C)$(ENABLE_LIBRDKAFKA) += serdes-kafka-avro-client
EXAMPLES_$(ENABLE_AVRO_CPP)$(ENABLE_LIBRDKAFKA) += kafka-serdes-avro-console-consumer
EXAMPLES_$(ENABLE_AVRO_CPP)$(ENABLE_LIBRDKAFKA) += kafka-serdes-avro-console-producer
EXAMPLES ?= $(EXAMPLES_y) $(EXAMPLES_yy)

all: $(EXAMPLES)

include ../mklove/Makefile.base

CFLAGS += -I/usr/local/include/libserdes
CXXFLAGS += -I/usr/local/include/libserdes

# lib must be compiled with -gstrict-dwarf, but examples must not,
# due to some clang bug on OSX 10.9
CPPFLAGS := $(subst strict-dwarf,,$(CPPFLAGS))

serdes-kafka-avro-client: serdes-kafka-avro-client.c
	$(CC) $(CPPFLAGS) $(CFLAGS) serdes-kafka-avro-client.c \
	-o $@ $(LDFLAGS) $(LIBS) -lrdkafka -lserdes

serdes-tool: serdes-tool.cpp
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) $^ \
	-o $@ $(LDFLAGS) $(LIBS) -lserdes++ -lserdes


kafka-serdes-avro-console-consumer: kafka-serdes-avro-console-consumer.cpp
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) $^ \
	-o $@ $(LDFLAGS) $(SLIB_CPP) $(SLIB) $(LIBS) -lrdkafka++ -lrdkafka -lserdes++ -lserdes

kafka-serdes-avro-console-producer: kafka-serdes-avro-console-producer.cpp
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) $^ \
	-o $@ $(LDFLAGS) $(LIBS) -lrdkafka++ -lrdkafka -lserdes++ -lserdes


clean:
	rm -f $(EXAMPLES)

