#!/usr/bin/env groovy
@Library('banzai@main') _

import static hudson.model.Result.*
import static io.werx.banzai.LogLevel.*


env.TRUE = 'true'
env.FALSE = 'false'
env.I_TRUE = '!true'
env.I_FALSE = '!false'

env.YES = "yes"
env.NO = "no"
env.I_YES = "!yes"
env.I_NO = "!no"


node() {

    properties( [
            parameters( [
                    booleanParam( name: "I_TRUE", defaultValue: false, description: "important environemment." ),
                    booleanParam( name: "I_FALSE", defaultValue: true, description: "important environment." ),
            ] )
    ] )

    stage( "Setup" ) {

        echo "Environment variables:"
        echo ""

        echo "Parameter variables:"
        echo ""

    }

    stage( "LogLevel Default" ) {
        log OFF, "LogLevel: OFF"
        log FATAL, "LogLevel: FATAL"
        log ERROR, "LogLevel: ERROR"
        log WARN, "LogLevel: WARN"
        log INFO, "LogLevel: INFO"
        log DEBUG, "LogLevel: DEBUG"
        log TRACE, "LogLevel: TRACE"
    }

    stage( "LogLevel OFF" ) {
        log.setLevel(OFF)
        log OFF, "LogLevel: OFF"
        log FATAL, "LogLevel: FATAL"
        log ERROR, "LogLevel: ERROR"
        log WARN, "LogLevel: WARN"
        log INFO, "LogLevel: INFO"
        log DEBUG, "LogLevel: DEBUG"
        log TRACE, "LogLevel: TRACE"
    }

    stage( "LogLevel TRACE" ) {
        log.setLevel(TRACE)
        log OFF, "LogLevel: OFF"
        log FATAL, "LogLevel: FATAL"
        log ERROR, "LogLevel: ERROR"
        log WARN, "LogLevel: WARN"
        log INFO, "LogLevel: INFO"
        log DEBUG, "LogLevel: DEBUG"
        log TRACE, "LogLevel: TRACE"
    }

    stage( "By Method" ) {
        log.fatal( "fatal message." )
        log.error( "error message." )
        log.warn( "warn message." )
        log.info( "info message" )
        log.debug( "debug message." )
    }

}
