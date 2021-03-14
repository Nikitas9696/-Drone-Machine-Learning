# Χαρτογράφηση Και Γεωγραφικός Εντοπισμός Ζημιών του Οδοστρώματος Με Χρήση Drone(Σμηα) και Machine Learning

<p align="center">
  <img width="400" height="400" src="https://user-images.githubusercontent.com/38980233/111069476-e502d280-84d5-11eb-8935-671c62c0d074.jpeg">
</p>

<p align="center">


<a>
  Όνομα Ομάδας : Master Builders

Μέλη Ομάδας : 
Βαρσαμάς Θεολόγιος, 
Ελευθεριάδης Νικόλαος  

Μέντορες Ομάδας : 
Παπαζήσης Παναγιώτης,  
Βαρσαμάς Νικήτας
  <a/>

</p>



## Περίληψη 
Στα πλαίσια της ανάπτυξης έξυπνης πόλης δημιουργούνται διαρκώς καινοτόμα συστήματα με τη χρήση του διαδικτύου έχοντας ως στόχο τη βελτίωση της υγείας, της ασφάλειας αλλά και τη γενικότερη πρόοδο της ποιότηταςζωής των ανθρώπων. Στόχος του συγκεκριμένου project είναι ο σχεδιασμός ενός συστήματος για την ανάλυση των αστικών και μη οδοστρωμάτων για την χαρτογράφηση, την αναγνώριση και τον γεωγραφικό εντοπισμό βλαβών με την χρήση εναέριων φωτογραφιών από αυτόνομο μη επανδρωμένο αεροσκάφος (ΣμηΕΑ). Η μέθοδος με την οποία εκτελείται η παραπάνω λειτουργιά περιλαμβάνει (i) τη διαδικασία δειγματοληψίας των φωτογραφιών μέσω του ΣμηΕΑ Parrot Anafi, (ii) την εκπαίδευση ενός συστήματος βαθιάς εκμάθησης (Deep Learning) για την αναγνώριση των βλαβών του οδοστρώματος αξιοποιώντας σύγχρονες τεχνικές και αλγορίθμους νευρωνικών δικτύων. Μετά την εκπαίδευση του συστήματος, θα λάβουν χώρα προγραμματισμένες πτήσεις σε συγκεκριμένες περιοχές της πόλης με σκοπό τη δημιουργία 3D ή 2D χαρτών μέσω του λογισμικού Pix4D Mapper. Ταυτόχρονα, πραγματοποιείται ο γεωγραφικός εντοπισμός της εκάστοτε βλάβης (παράδειγμα επικίνδυνη λακκούβα στο δρόμο) με γεωγραφικές συντεταγμένες (Latitude, Longitude). Μετά το πέρας της παραπάνω διαδικασίας, τα δεδομένα στέλνονται σε μια βάση δεδομένων που αναπτύχθηκε στο περιβάλλον Firebase και απεικονίζονται σε σελίδα που αναπτύχθηκε με τη βιβλιοθήκη React της γλώσσας προγραμματισμού JavaScript. Επιπροσθέτως, μέσω του Google Maps API, στο προαναφερόμενο σύστημα απεικονίζονται οι περιοχές που έχουν πραγματοποιηθεί οι πτήσεις καθώς και τα εκτιμόμενα αναγνωρισμένα σημεία.
 
## Ανάλυση συστήματος
Στο παρακάτω διάγραμμα απεικονίζονται οι διακριτές ενέργειες για την υλοποίηση του προτεινόμενου συστήματος γδνδ.

<p align="center">
  <img width="400" height="400" src="https://user-images.githubusercontent.com/38980233/111069486-f1872b00-84d5-11eb-95e2-648c32c8f637.png">
</p>




# Συγκομιδή δεδομένων εκπαίδευσης
Η μηχανική μάθηση μπορεί να παράγει πολλά υποσχόμενα αποτελέσματα όταν υπάρχουν διαθέσιμα επαρκή δεδομένα εκπαίδευσης. Ωστόσο, για το συγκεκριμένο project δεν υπάρχουν εκπαιδευμένα μοντέλα που να απευθύνονται σε ζημιές ή βλάβες στο οδικό δίκτυο μιας πόλης. Λαμβάνοντας υπόψη το παραπάνω γεγονός, κρίνεται απαραίτητο να υπάρξει μεγάλος όγκος φωτογραφιών για την κατασκευή του μοντέλου. Για την πραγματοποίηση ενός τέτοιο εγχειρήματος, είναι σημαντικό τα δείγματα των εικόνων να είναι πολλά σε αριθμό αλλά ταυτόχρονα να υπάρχει ποικιλία από διαφορετικούς τύπους οδοστρώματος καθώς επίσης και από διαφορετικούς τύπους ζημιών. Πιο συγκεκριμένα, τα δείγματα θα πρέπει να έχουν φωτογραφηθεί υπό διαφορετικές γωνίες λήψης, σε διαφορετικό ύψος καθώς επίσης και σε διαφορετικές συνθήκες του περιβάλλοντος.
Εκπαίδευση νευρωνικού δικτύου
Μετά πέρας της διαδικασίας συλλογής των δεδομένων, λαμβάνει χώρα η διαδικασία της δημιουργίας της ταξινόμησης των δειγμάτων (labeling). Τα επεξεργασμένα πλέον δεδομένα μπορούν να μεταβιβαστούν στην επόμενη διαδικασία της κατηγοριοποίησης - ταξινόμησής (classification) των φωτογραφιών. Με τη βοήθεια των προαναφερόμενων δεδομένων, η ταξινόμηση σε προγράμματα μηχανικής μάθησης αξιοποιεί ένα ευρύ φάσμα αλγορίθμων για την ταξινόμηση μελλοντικών δεδομένων σε αντίστοιχες και σχετικές κατηγορίες. Μετά το πέρας της εκπαίδευσης του νευρωνικού δικτύου, ο προγραμματιστής ορίζει μια αποστολή αυτόνομης πτήσης σε μια περιοχή της πόλης για τη λήψη φωτογραφιών.

## Συγκομιδή δεδομένων επικύρωσης

Αφού φέρει εις πέρας την αποστολή οι αποθηκευμένες εικόνες που έκανε λήψη το ΣμηΕΑ φιλτράρονται μέσω του συστήματος της μηχανικής εκμάθησης που αναφέρθηκε νωρίτερα για τον εντοπισμό τυχών βλαβών του οδοστρώματος. Στις εικόνες αυτές υπάρχει η πληροφορία των γεωγραφικών συντεταγμένων που βρέθηκε η ζημιά.

## Ενημέρωση Πληροφοριακού συστήματος (ιστοσελίδας)

Τέλος, οι εικόνες αυτές εισάγονται στην βάση δεδομένων του Firebase, και απεικονίζονται οι ίδιες στην σελίδα που αναπτύχθηκε στο περιβάλλον της βιβλιοθήκης React. Ταυτόχρονα με αυτή την διαδικασία γίνεται και η παραγωγή 2D ή 3D χάρτη των περιοχών που το ΣμηΕΑ έχει φωτογραφίσει.

## Στόχος του συστήματος

Στόχος του συστήματος στα πλαίσια της έξυπνης πόλης είναι η ενημέρωση των χρηστών της για ζημίες στο οδόστρωμά να γνωρίζουν άμεσα τα σημεία που ο δρόμος απαιτεί επιδιόρθωση. Τα αποτελέσματα των παραπάνω γεγονότων οδηγούν στα εξής αποτελέσματα:

- Μείωση των ατυχημάτων στο οδικό δίκτυο.
- Μείωση των αποζημιώσεων στους ιδιοκτήτες των οχημάτων που έχουν υποστεί υλικές ζημιές στα περιουσιακά τους στοιχεία, λόγω της κακής ποιότητας του οδικού                       δικτύου.
- Αύξηση της εμπιστοσύνης των πολιτών απέναντι στις δημόσιες αρχές λόγω της συνέπειας τους για την συνεχή αύξηση του επιπέδου ασφάλειας του οδικού δικτύου.




## Μελλοντικά σχέδια

Το συγκεκριμένο project είναι πολλά υποσχόμενο για μελλοντικές αναβαθμίσεις με γνώμονα πάντα την αύξηση της ποιότητας της ζωής των ανθρώπων. Κάποια από τα μελλοντικά σχέδια είναι τα εξής:

- Αναλυτική ενημέρωση των πολιτών, για την έναρξη των διαδικασιών συντήρησης ενός δρόμου καθώς επίσης και το χρονικό διάστημα που απαιτείται για την         επιδιόρθωση του.
- Καταμέτρηση των οχημάτων αλλά και του συνολικού φορτίου που έχει διασχίσει το οδόστρωμα σε πραγματικό χρόνο, με στόχο την ανάπτυξη μοντέλου υπολογισμού          της καταπόνησης του οδοστρώματος αλλά και πρόβλεψης για το πότε θα χρειαστεί επισκευή προληπτικά. Με αυτόν τον τρόπο θα μειωθεί ακόμα περισσότερο το κόστος        συντήρησης του οδοστρόματος.


## Για την υλοποίηση του Project είναι απαραίτητα τα παρακάτω υλικά:
- [x] Drone(Σμηα) Parrot Anafi: https://www.homelike.gr/paichnidia/parrot-anafi-pf728000.html?
- [x] Μαξιλάρι προσγείωσης Σμηα (Landing Pad) : https://www.copters.gr/pgytech-drone-landing-pad-55cm.html



