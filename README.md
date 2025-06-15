import csv

def clean_csv(input_file, output_file):
    try:
        with open(input_file, mode='r', newline='', encoding='utf-8') as infile:
            reader = csv.reader(infile)
            rows = list(reader)

  cleaned_rows = []
  seen = set()
  removed_count = 0

  for row in rows:
       # Skip empty rows (all fields empty or whitespace)
    if not any(cell.strip() for cell in row):
          removed_count += 1
                continue

            # Remove duplicates
  row_tuple = tuple(cell.strip() for cell in row)  
  # strip to avoid whitespace duplicates
  if row_tuple not in seen:
            seen.add(row_tuple)
            cleaned_rows.append(row)
  else:
            removed_count += 1

        # Write cleaned data to output file
  with open(output_file, mode='w', newline='', encoding='utf-8') as outfile:
            writer = csv.writer(outfile)
            writer.writerows(cleaned_rows)

  print(f"Cleaning complete. {removed_count} rows removed.")
        print(f"Cleaned file saved as '{output_file}'.")

  except FileNotFoundError:
        print(f"Error: File '{input_file}' not found.")
    except Exception as e:
        print(f"An error occurred: {e}")

# Example usage
if __name__ == "__main__":
    input_csv = input("Enter the input file")
    output_csv = input("Enter the ouput file: ")
    clean_csv(input_csv, output_csv)
