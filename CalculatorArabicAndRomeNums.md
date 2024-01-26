    import java.util.Scanner;

    public class CalculatorWithRomeNumbers {

    public static void main(String[] args) throws Exception {
        while (true) {
            Scanner sc = new Scanner(System.in);
            String input = sc.nextLine();
            check(input);
            calc(input);
        }
    }
    public static String calc(String input) throws Exception {
        input = input.replaceAll("\\s", "");
        char operation = input.replaceAll("[^\\+\\-\\*\\/]", "").charAt(0);
        String[] numbers = input.split("[\\+\\-\\*\\/]");
        String calc = null;
        String resultRoman = null;
        if (convertRtoA(numbers[0]) != -1) {
            int var1 = convertRtoA(numbers[0]);
            int var2 = convertRtoA(numbers[1]);
            if (var1 < 0 || var2 < 0) {
                System.out.println("Введены числа из двух разных систем");
                System.exit(0);
            } else {
                String result = operations(operation, var1, var2);
                resultRoman = convertAtoR(Integer.parseInt(result));
                System.out.println(resultRoman);
            }
            return resultRoman;
        } else {
               try {
                   int number1 = Integer.parseInt(numbers[0]);
                   int number2 = Integer.parseInt(numbers[1]);
                   calc = operations(operation, number1, number2);
                   System.out.println(calc);
               }catch (Exception e){
                   System.out.println("Введены числа из двух разных систем");
                   System.exit(0);
               }
            }
        return calc;
    }

    static String operations(char operation, int number1, int number2) throws Exception {
        int result = 0;
        if ((number1 >= 1 && number1 <= 10) && (number2 >= 1 && number2 <= 10)) {
            switch (operation) {
                case '+':
                    result = number1 + number2;
                    break;
                case '-':
                    result = number1 - number2;
                    break;
                case '*':
                    result = number1 * number2;
                    break;
                case '/':
                    result = number1 / number2;
                    break;
            }
            return Integer.toString(result);
        } else {
            System.out.println("Введено неверное число");
            System.exit(0);
        }
        return null;
    }
    static void check(String input) throws Exception {
        int count = 0;
        try {
            for (char c : input.toCharArray()) {
                if (c == '+' || c == '-' || c == '*' || c == '/') {
                    count++;
                }
            }
                if (count != 1) {
                    throw new Exception();
                }
        }catch(Exception e){
            if(count > 1) {
                System.out.println("В выражении может использоваться только один аримфметический оператор");
                System.exit(0);
            }if (count < 1){
                System.out.println("Введите арифметическое выражение");
                System.exit(0);
            }
            }
    }
    static String convertAtoR (int numArabian) throws Exception {
        if (numArabian < 0) {
            System.out.println("Римское число не может быть отрицательным");
            System.exit(0);
        } else {
            int[] arabic = {1, 4, 5, 9, 10, 40, 50, 90, 100};
            String[] roman = {"I", "IV", "V", "IX", "X", "XL", "L", "XC", "C"};
            StringBuilder result = new StringBuilder();
            int i = arabic.length - 1;
            while (numArabian > 0) {
                if (numArabian - arabic[i] >= 0) {
                    result.append(roman[i]);
                    numArabian -= arabic[i];
                } else {
                    i--;
                }
            }
            return result.toString();
        }
        return null;
    }
    static int convertRtoA(String numRoman) throws Exception {
            switch (numRoman) {
                case "I" -> {
                    return 1;
                }
                case "II" -> {
                    return 2;
                }
                case "III" -> {
                    return 3;
                }
                case "IV" -> {
                    return 4;
                }
                case "V" -> {
                    return 5;
                }
                case "VI" -> {
                    return 6;
                }
                case "VII" -> {
                    return 7;
                }
                case "VIII" -> {
                    return 8;
                }
                case "IX" -> {
                    return 9;
                }
                case "X" -> {
                    return 10;
                }
            }
        return -1;
    }
}
