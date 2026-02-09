import java.math.BigDecimal;
import java.math.RoundingMode;

public class WesternUnionExactQuote {

    public static void main(String[] args) {

        // Fixed deterministic inputs
        BigDecimal sendAmount = new BigDecimal("100.00");   // USD
        BigDecimal fee = new BigDecimal("2.99");            // USD fixed fee
        BigDecimal fxRate = new BigDecimal("83.2500");      // USD -> INR fixed rate

        // Step 1: Net send after fee
        BigDecimal netSend = sendAmount.subtract(fee).setScale(2, RoundingMode.HALF_UP);

        // Step 2: Receiver gets (exact calculation)
        BigDecimal receiverGets = netSend.multiply(fxRate).setScale(2, RoundingMode.HALF_UP);

        // Step 3: Total debit from sender (send amount only, fee already included in breakdown)
        BigDecimal totalDebit = sendAmount.setScale(2, RoundingMode.HALF_UP);

        // Exact Output (Always same)
        System.out.println("=== Western Union FX Quote (Exact Result) ===");
        System.out.println("Send Amount (USD): " + sendAmount);
        System.out.println("Fee (USD): " + fee);
        System.out.println("FX Rate (USD->INR): " + fxRate);
        System.out.println("Receiver Gets (INR): " + receiverGets);
        System.out.println("Total Debit (USD): " + totalDebit);
    }
}
