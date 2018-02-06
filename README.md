# example-log-processor

Log processor which might be needed on each api calling to print all the payloads.

example:

package com.sjabonir;

import org.apache.camel.Exchange;
import org.apache.camel.Processor;
import org.slf4j.LoggerFactory;

import java.util.Map;

/**
 * Created by shadrach.jabonir on 12/13/2016.
 */

public class LoggerProcessor implements Processor {
    private static final org.slf4j.Logger log = LoggerFactory.getLogger(LoggerProcessor.class);

    @Override
    public void process(Exchange exchange) throws Exception {
        try{
            Map<String, Object> headers = exchange.getIn().getHeaders();
            //header
            for(Map.Entry<String, Object> e : headers.entrySet()) {
                log.debug("Got message with header -> " + e.getKey() + " : " + e.getValue().toString());
            }
            //body
            log.debug("Got message with body : " + exchange.getIn().getBody(String.class));
        }catch(Exception e){
            log.error("Got message but error : " + e.getMessage());
        }

    }
}
