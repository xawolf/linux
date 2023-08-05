#!/bin/bash

start_dir="/var/lib/docker/"
container_logs=($(find "$start_dir" -type f -name "*.log"))
total_logs=${#container_logs[@]}

# Function to display a progress bar
progress_bar() {
    local current=$1
    local total=$2
    local percentage=$((current * 100 / total))
    local completed=$((percentage / 2)) # Adjust this for the size of the progress bar

    printf "\r["
    printf "%*s" "$completed" "" | tr ' ' '#'
    printf "%*s" "$((50 - completed))" ""
    printf "] %3d%%" "$percentage"
}

for ((i=0; i<$total_logs; i++)); do
    log="${container_logs[i]}"
    tail -n 100 "$log" > "$log.temp"
    mv "$log.temp" "$log"
    echo "$log truncated"

    progress_bar $((i+1)) $total_logs
done

# Print a new line to separate the progress bar from subsequent output
echo
