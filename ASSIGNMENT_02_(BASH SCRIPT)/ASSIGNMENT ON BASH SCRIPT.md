# BASH SCRIPT

## TASK
1. Write a shell script that checks the disk usage in a given directory. The script can take two optional arguments and one compulsory argument...
-d: which means that all files and directory within the specified directory or directories should be listed.
-n: which means that the top N enteries should be returned.
list of directories: this will be the directories you want to check it's disk usage

eg yourscript.sh -n 5 /var
should return the top 5 directories wrt disk usage in /var directory

yourscript.sh -d /var
should list both directories and files

Note: if -n argument is not given, it should return 8 enteries by default.

2. Create a backup script. This script creates a backup of a given directory and saves it in another directory with a timestamp. It takes two arguments:
the source directory and the destination directory

Note: The backup should be a tar archive

## SOLUTION
> 1. check_disk_usage.sh
```
#!/bin/bash

# Define default number of entries
DEFAULT_ENTRIES=8

# Parse arguments
while getopts ":d:n:" opt; do
  case $opt in
    d)
      # Set flag for detailed listing
      LIST_DETAILS=true
      ;;
    n)
      # Set number of entries from argument
      NUM_ENTRIES=$OPTARG
      ;;
    \?)
      echo "Invalid option: -$OPTARG" >&2
      exit 1
      ;;
  esac
done

# Shift arguments to remove options
shift $((OPTIND-1))

# Check if directory argument is provided
if [[ $# -eq 0 ]]; then
  echo "Error: Please provide a directory to check." >&2
  exit 1
fi

# Get directory path
dir_path="$1"

# Use `du` command with appropriate options
if [[ $LIST_DETAILS ]]; then
  # List details (files and directories)
  command="du -sh"
else
  # Summarize disk usage by directory
  command="du -s"
fi

# Add path argument
command="$command $dir_path/*"

# Sort by size (descending) and potentially limit entries
sorted_output=$(eval "$command" | sort -nr | head -n "${NUM_ENTRIES:-$DEFAULT_ENTRIES}")

# Print results
echo "Top $(( ${NUM_ENTRIES:-$DEFAULT_ENTRIES} )) entries for disk usage in $dir_path:"
echo "$sorted_output"
```

> 2. create_backup.sh
```
#!/bin/bash

# Check if two arguments are provided
if [[ $# -ne 2 ]]; then
  echo "Error: Please provide source and destination directories." >&2
  exit 1
fi

# Get source and destination paths
source_dir="$1"
dest_dir="$2"

# Check if source directory exists
if [[ ! -d "$source_dir" ]]; then
  echo "Error: Source directory '$source_dir' does not exist." >&2
  exit 1
fi

# Create timestamp for backup filename
timestamp=$(date +"%Y-%m-%d_%H-%M-%S")

# Build destination filename with timestamp
dest_file="$dest_dir/backup_$source_dir\_$timestamp.tar.gz"

# Create the backup archive using `tar` command
tar -czf "$dest_file" "$source_dir"

# Print success message
echo "Backup created successfully: $dest_file"
```