    import java.util.Scanner;

    public class Calculator {
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
        try {
            int number1 = Integer.parseInt(numbers[0]);
            int number2 = Integer.parseInt(numbers[1]);
            calc = operations(operation, number1, number2);
            System.out.println(calc);
            }catch (Exception e){
                System.out.println("Введено неверное число");
                System.exit(0);
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
        for (char c : input.toCharArray()) {
            if (c == '+' || c == '-' || c == '*' || c == '/') {
                count++;
            }
        }
        if (count >1) {
            System.out.println("В выражении должно использоваться не более двух операндов и одного оператора");
            System.exit(0);
        }if (count < 1){
            System.out.println("Введите арифметическое выражение");
            System.exit(0);
        }
    }
}