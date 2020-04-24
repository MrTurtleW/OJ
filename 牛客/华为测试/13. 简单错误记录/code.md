```python
class Record:
    def __init__(self, filename, line_num):
        self.filename = filename
        self.line_num = line_num
        self.count = 1


class Records:
    def __init__(self):
        self.records = []

    def find_record(self, filename, line_num):
        for index, record in enumerate(self.records):
            if record.filename == filename and record.line_num == line_num:
                return index

        return -1

    def add(self, filename, line_num):
        if '\\' in filename:
            filename = filename.split('\\')[-1]

        index = self.find_record(filename, line_num)
        if index >= 0:
            record = self.records[index]
            record.count += 1

        else:
            self.records.append(Record(filename, line_num))
            self.records = self.records

    def print(self):
        for record in self.records[-8:]:
            print(record.filename[-16:], record.line_num, record.count)


try:
    records = Records()
    while True:
        filename, line_num = input().split()
        records.add(filename, line_num)

except:
    # import traceback;traceback.print_exc()
    records.print()
```