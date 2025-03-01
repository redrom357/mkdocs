```bash
#!/bin/bash

# Function to convert blocks to terabytes
blocks_to_tb() {
  local blocks=$1
  local tb=$(bc -l <<< "scale=4; ($blocks * 512) / (1024 ^ 4)")
  echo "$tb"
}

# Function to convert terabytes to blocks
tb_to_blocks() {
  local tb=$1
  local blocks=$(bc -l <<< "scale=0; ($tb * (1024 ^ 4)) / 512")
  echo "$blocks"
}

# Main function
main() {
  while true; do
    echo "Block and Terabyte Converter"
    echo "---------------------------"
    echo "1. Convert blocks to terabytes"
    echo "2. Convert terabytes to blocks"
    echo "3. Quit"
    read -p "Choose an option: " option

    case $option in
      1)
        read -p "Enter the number of blocks: " blocks
        tb=$(blocks_to_tb $blocks)
        echo "$blocks blocks is equal to $tb TB"
        ;;
      2)
        read -p "Enter the number of terabytes: " tb
        blocks=$(tb_to_blocks $tb)
        echo "$tb TB is equal to $blocks blocks"
        ;;
      3)
        echo "Goodbye!"
        exit 0
        ;;
      *)
        echo "Invalid option. Please choose a valid option."
        ;;
    esac
  done
}

main
```