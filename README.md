# POSIX-threads-Multiple-Change-Detector-RTES-2015
 Σκοπός της άσκησης είναι να αναζητηθεί η οριακή συμπεριφορά του υπολoγιστή σε πραγματικό χρόνο. Το πρόγραμμα που δίνεται στην εκφώνηση της εργασίας αναγνωρίζει την αλλαγή ενός σήματος από 0 σε 1 χρησιμοποιώντας ένα νήμα ελέγχου. Το ζητούμενο είναι να αναγνωριστούν περισσότερα σήματα στον ίδιο χρόνο. Προκειμένου να βελτιστοποιηθεί η διαδικασία είναι επιβεβλημένο να χρησιμοποιήσουμε τις δυνατότητες του υπολογιστή στο μέγιστο. Για το λόγο αυτό χρησιμοποιούμε POSIX Threads, ώστε οι πολλαπλοί πυρήνες του υπολογιστή να ελέγχουν ταυτόχρονα περισσότερα σήματα και να επιτευχθεί ο ελάχιστος χρόνος αναγνώρισης.

```
Example:
2 Threads & 120 Signals & Change frequency 1.0 s 
Changed: 29 detected: 29  
Real time Detection time: 1 μs  
Mean Detection Time: 0 μs and Standard deviation: 0 μs 
Value Range: 1 μs
```

 Στην συνάρτηση main() εκκινούμε πολλαπλά νήματα με την συνάρτηση ChangeDetector(). Η συνάρτηση SensorSignalReader() παραμένει αμετάβλητη. Κάθε νήμα ελέγχει έναν συγκεκριμένο αριθμό σημάτων από τον πίνακα signalArray(). Στην πραγματικότητα διανέμουμε τον αριθμό σημάτων στα νήματα ώστε να γίνει καλύτερη διαχείρηση του υλικού και να επιτευχθεί η βέλτιστη συμπεριφορά. Η λογική με την οποία κατατάσσουμε τα σήματα είναι η εξής:
1. Κάθε σήμα πρέπει να αντιστοιχεί σε ένα, και μόνο ένα, νήμα.
2. Ένα (μόνο ένα) νήμα δεν πρέπει να ελέγχει περισσότερα σήματα από τα υπόλοιπα.
3. Αν ένα νήμα δεν ελέγχει κάποιο κελί, τότε τερματίζεται.
4. Αν ο αύξων αριθμός του νήματος είναι μεγαλύτερος από τον αριθμό των σημάτων, το νήμα τερματίζεται.
