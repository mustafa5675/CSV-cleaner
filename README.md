    # CSV-cleaner
    # Simple python script that cleans a CSV file by removing empty and duplicate rows
import csv

def clean_csv(input_file, output_file):
  rows_seen = set()
  cleaned_rows = []

    # Read the CSV and store non-duplicate, non-empty rows
  with open(input_file, 'r', newline='') as infile:
    reader = csv.reader(infile)
    header = next(reader, None)
    if header:
      cleaned_rows.append(header)
    for row in reader:
            # Check if the row is completely empty
      if not any(cell.strip() for cell in row):
        continue
            # Use tuple of row for duplicate check
        row_tuple = tuple(row)
        if row_tuple not in rows_seen:
          cleaned_rows.append(row)
          rows_seen.add(row_tuple)

    # Write cleaned rows to output file
  with open(output_file, 'w', newline='') as outfile:
    writer = csv.writer(outfile)
    writer.writerows(cleaned_rows)
    print(f"Cleaned CSV saved to {output_file}")

if __name__ == "__main__":
  input_path = input("Enter the path to your CSV file: ").strip()
  output_path = input("Enter the path to save the cleaned CSV file: ").strip()
  clean_csv(input_path, output_path)
