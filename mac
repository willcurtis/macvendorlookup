#!/bin/bash

  rawurlencode() {
    local string="${1}"
    local strlen=${#string}
    local encoded=""
    local pos c o

    for (( pos=0 ; pos<strlen ; pos++ )); do
       c=${string:$pos:1}
       case "$c" in
          [-_.~a-zA-Z0-9] ) o="${c}" ;;
          * )               printf -v o '%%%02x' "'$c"
       esac
       encoded+="${o}"
    done
    ENC="${encoded}"
  }


  OUI=${1:?'bad mac'}
  rawurlencode $OUI
  response=$(curl -s "https://api.macvendors.com/$ENC")
  if [ "$response" = '{"errors":{"detail":"Page not found"}}' ];
  then
      printf "MAC: $OUI\nVendor: Not Found"
  else
      printf  "MAC: $OUI\nVendor: $response"
  fi
  printf "\n"
