#!/usr/bin/env groovy
@Library('banzai@main') _

import hudson.model.Result

import static hudson.model.Result.*


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

    // Reused variables:
    int pauses = 0
    int tries = 0

    stage( "Setup" ) {

        echo "Environment variables:"
        echo ""

        echo "Parameter variables:"
        echo ""

    }

    stage( "bad args tests" ) {

        echo "No parameters specified."
        try {
            retryUntil( )
        } catch ( Exception e ) {
            echo "Exception thrown:"
            echo "${e.message}"
        }

        echo "Neither maxTries or maxTime not specified."
        try {
            retryUntil( task: { 0 } )
        } catch ( Exception e ) {
            echo "Exception thrown:"
            echo "${e.message}"
        }

    }

    stage( "maxTries 3 .. 1" ) {

        echo "Can try 3 times..."
        def times = 3
        retryUntil( maxTries: 3, task: { --times } )

        echo "Can try 2 times..."
        times = 2
        retryUntil( maxTries: 2, task: { --times } )

        echo "Can try 1 times..."
        times = 1
        retryUntil( maxTries: 1, task: { --times } )

    }

    stage( "maxTime" ) {

        echo "maxTime (10S) reached before success..."
        try {
            retryUntil( maxTime: "PT10S", pauseFor: "PT2S", task: {
                // echo "Test: maxTime reached before success..."
                1
            } )
        } catch ( Exception ex ) {
            if ( ex.message == "No success after waiting PT10S time." ) {
                echo "${ex.message}"
                echo "Test: SUCCESS."
            } else {
                throw ex
            }
        }

        echo "maxTime (10S) NOT reached before success..."
        pauses = 0
        retryUntil( maxTime: "PT10S", pauseFor: "PT2S", task: {
            pauses++
            /// echo "Test: maxTime NOT reached before success ${pauses}."
            if ( pauses > 5 ) {
                echo "Test: SUCCESS."
                0
            } else {
                1
            }
        } )

        echo "maxTime (10S) reached before maxTries (11)..."
        tries = 0
        try {
            // Times out in 10s, but will try 11 times, pausing 1s each try.
            retryUntil( maxTime: "PT10S", maxTries: 11, pauseFor: "PT1S", task: {
                tries++
                // echo "Iteration: ${pauses}."
                if ( tries > 11 ) {
                    echo "Test: FAILURE."
                    0
                } else {
                    1
                }
            } )
        } catch ( Exception ex ) {
            if ( ex.message == "No success after waiting PT10S time." ) {
                echo "${ex.message}"
                echo "Test: SUCCESS."
            } else {
                throw ex
            }
        }

        echo "maxRetries (10) reached before maxTime (12S)..."
        tries = 0
        try {
            retryUntil( maxTime: "PT12S", maxTries: 10, pauseFor: "PT1S", task: {
                tries++
                // echo "Iteration: ${pauses}."
                if ( tries == 10 ) {
                    echo "Test: SUCCESS."
                    0
                } else {
                    1
                }
            } )
        } catch ( Exception ex ) {
            if ( ex.message == "No success after waiting PT12S time." ) {
                echo "${ex.message}"
                echo "Test: FAILURE."
            } else {
                throw ex
            }
        }

    }

}
