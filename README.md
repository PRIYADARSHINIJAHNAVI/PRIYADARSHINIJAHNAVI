- 👋 Hi, I’m @PRIYADARSHINIJAHNAVI
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
PRIYADARSHINIJAHNAVI/PRIYADARSHINIJAHNAVI is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import java.io.*;
import java.awt.Point;
import java.util.HashMap;
import java.util.Scanner;
 
public class CSV {
 
    private HashMap<Point, String> _map = new HashMap<Point, String>();
    private int _cols;
    private int _rows;
 
    public void open(File file) throws FileNotFoundException, IOException {
        open(file, ',');
    }
 
    public void open(File file, char delimiter)
            throws FileNotFoundException, IOException {
        Scanner scanner = new Scanner(file);
        scanner.useDelimiter(Character.toString(delimiter));
 
        clear();
 
        while(scanner.hasNextLine()) {
            String[] values = scanner.nextLine().split(Character.toString(delimiter));
 
            int col = 0;
            for ( String value: values ) {
                _map.put(new Point(col, _rows), value);
                _cols = Math.max(_cols, ++col);
            }
            _rows++;
        }
        scanner.close();
    }
 
    public void save(File file) throws IOException {
        save(file, ',');
    }
 
    public void save(File file, char delimiter) throws IOException {
        FileWriter fw = new FileWriter(file);
        BufferedWriter bw = new BufferedWriter(fw);
 
        for (int row = 0; row < _rows; row++) {
            for (int col = 0; col < _cols; col++) {
                Point key = new Point(col, row);
                if (_map.containsKey(key)) {
                    bw.write(_map.get(key));
                }
 
                if ((col + 1) < _cols) {
                    bw.write(delimiter);
                }
            }
            bw.newLine();
        }
        bw.flush();
        bw.close();
    }
 
    public String get(int col, int row) {
        String val = "";
        Point key = new Point(col, row);
        if (_map.containsKey(key)) {
            val = _map.get(key);
        }
        return val;
    }
 
    public void put(int col, int row, String value) {
        _map.put(new Point(col, row), value);
        _cols = Math.max(_cols, col+1);
        _rows = Math.max(_rows, row+1);
    }
 
    public void clear() {
        _map.clear();
        _cols = 0;
        _rows = 0;
    }
 
    public int rows() {
        return _rows;
    }
 
    public int cols() {
        return _cols;
    }
 
    public static void main(String[] args) {
        try {
            CSV csv = new CSV();
 
            csv.open(new File("test_in.csv"));
            csv.put(0, 0, "x");
            csv.put(0, 1, "y");
            csv.save(new File("test_out.csv"));
        } catch (Exception e) {
        }
    }
}
2 bool positive = number > 0;
bool negative = number < 0;
float number =0;
