==============================================================================
  Posse Score
  By Guns Goforth
==============================================================================

What is Posse Score?
--------------------

Posse Score is a scoring program for Cowboy Action Shooting matches. The
program is licensed under the MIT License, which means you are free to use
it but must contribute back to the open source project if you improve it.


Why Posse Score?
----------------

I developed Posse Score because I saw that existing software didn't go the
whole mile in the administration of an entire match. The software out there
was either oriented mostly toward other shooting sports and didn't receive
much attention, or it was a one-trick pony designed only for smaller matches.

Another problem is that other programs were dedicated to tablet use only,
which makes them awkward for analyzing data at a large match. One important
problem with some commercial platforms is that you don't truly own your own
data. When it comes time to award prizes and produce final reports, you end
up back at manual entry. This all creates huge problems for match
administrators, who tackle it head-on — fortunately for the sport.


How Does Posse Score Solve These Problems?
------------------------------------------

The main reason Posse Score is better is that it doesn't try to cram all
of the match management features into one application on a tablet. A tablet
is useful as a scoring device but awkward for administration. Posse Score
divides the problem into two parts: scoring and administration.

The web server interface runs on any tablet or phone and is optimized for
the scoring person at the firing line. The command line interface handles
administration and can also run on a tablet, but is better suited to a
computer. A small laptop or Raspberry Pi works fine — the program takes
very little in the way of computer resources.

In addition to dividing the problem into manageable, optimized parts,
Posse Score goes a step further by using a database to store information.
By using the SQLite database, there is a great deal of flexibility in
match administration. For example, reports can be designed and printed,
and email mailing lists can be exported. The program also outputs results
in CSV format, which almost all spreadsheets can read and write. Match
contestants can be read into the program using this same simple format —
just use a spreadsheet to enter the data and the program will load them
into the shadow shooter database, where they will be ready the next time
you need to start a match.


How Does It Work?
-----------------

Posse Score can work as a simple command line program on your computer with
all of the features available. You can also start the web interface, and any
tablet, computer, or cell phone can open the URL to access the program
through a graphical interface optimized for ease of use by the scoring
person.

In this mode, a WiFi network links all of the tablets to the administration
base computer. All of the data is stored in one location — no syncing of
devices is needed. There is also a standalone mode where everything can be
done on an Android tablet without the use of a WiFi network.

The network does not need to be connected to the internet. An inexpensive
WiFi router will do the job. The only thing you need to be aware of is that
you may need to disable the firewall on the host computer so the tablets
can communicate with the server.


Conclusion
----------

Posse Score is a comprehensive solution to the problem of scoring and
administration of a Cowboy Action Shooting match. It was created as an
open source project meant to be a lasting solution and a gift to the sport
of Cowboy Action Shooting.


Can You Return the Favor?
-------------------------

As you are all aware, the shooting sports are under constant attack, and
California is fighting for dear life just to survive. If you find this
program useful, can you return the favor and provide a donation to our
Ukiah gun club, which has been fighting lawsuits for decades? Please send
your donation to the following address. If you can make a note on the check
that says "Posse Score Donation," that would let them know why you are
sending it.

Make checks out to:

  Ukiah Rifle and Pistol Club
  P.O. Box 26
  Ukiah, CA 95482

==============================================================================
