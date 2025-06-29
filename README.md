import csv

def clean_csv_file(input_file, output_file=None, remove_duplicates=True, drop_empty_rows=True):
    """
    Cleans a CSV file by:
    - Stripping whitespace from headers and values
    - Converting headers to UPPERCASE and replacing spaces with underscores
    - Optionally removing duplicate rows
    - Optionally dropping rows with empty fields
    Saves the cleaned CSV to the specified output file.
    If output filename is not provided, it will be generated automatically.
    """
    # Generate output filename if not provided
    if output_file is None:
        if input_file.lower().endswith('.csv'):
            output_file = 'cleaned_' + input_file[:-4] + '.csv'
        else:
            output_file = 'cleaned_' + input_file + '.csv'
    
    cleaned_rows = []
    seen_rows = set()

    with open(input_file, mode='r', newline='', encoding='utf-8') as infile:
        reader = csv.reader(infile)
        rows = list(reader)

    if not rows:
        print("The CSV file is empty.")
        return

    # Clean header: UPPERCASE and replace spaces with underscores
    raw_header = rows[0]
    header = [col.strip().upper().replace(' ', '_') for col in raw_header]

    for row in rows[1:]:
        cleaned_row = [cell.strip() for cell in row]

        # Skip rows with empty values or mismatched length
        if drop_empty_rows and ('' in cleaned_row or len(cleaned_row) != len(header)):
            continue

        row_tuple = tuple(cleaned_row)
        if remove_duplicates and row_tuple in seen_rows:
            continue

        seen_rows.add(row_tuple)
        cleaned_rows.append(cleaned_row)

    with open(output_file, mode='w', newline='', encoding='utf-8') as outfile:
        writer = csv.writer(outfile)
        writer.writerow(header)
        writer.writerows(cleaned_rows)

    print(f"Cleaned CSV written to: {output_file}")

if __name__ == "__main__":
    input_csv = input("Enter the path of the CSV file to clean: ").strip()
    output_csv = input("Enter the desired output file path (press Enter to use default): ").strip()
    output_csv = output_csv if output_csv else None
    clean_csv_file(input_csv, output_csv)
