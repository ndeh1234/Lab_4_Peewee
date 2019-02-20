# Lab_4_Peewee

from peewee import *

db = SqliteDatabase('Chainsaw_Juggling_Recorders_Holders.sqlite')


class Records_Holders(Model):

     name = CharField()
     country = CharField()
     catches = IntegerField()

class Meta:
    database = db;

    def __str__(self):
        return f'{self.name} is a {self.country} records_holders and is {self.catches}'

    # connect to DB and creates a table that maps to the model records_holders

    db.connect()
    db.create_tables([Records_Holders])

    # Creates record holder objects and call save function to insert them into database

    print('\nCreate and saves 3 records holders')
    IanStewart = Records_Holders(name = "Ian Stewart", country='Canada', catches = 94)
    IanStewart.save()

    AaronGregg = Records_Holders(name="AaronGregg", country='Canada',  catches=88)
    AaronGregg.save()

    ChadTaylor = Records_Holders(name="ChadGregg", country='USA', catches=78)
    ChadTaylor.save()


print('\nFind all records holders')

records_holders = Records_Holders.select()

for records_holder in records_holders:
    print(records_holder)

ChadTaylor.country = 'Mexico'

ChadTaylor.save()

print('\n Chad Taylor now lives in:, Chad Taylor')

# Adding another records holder

print('\nAdd new record holder')

TataPeter = Records_Holders(name="TataPeter", country='France', catches=70)
TataPeter.save()

print(TataPeter)



def search_for_record_holder(self, term):
    # Searches the recorder holder table for a name.

    try:
        cur = self._db.cursor()
        search = f'%{name.upper()}%'
        cur.execute('SELECT rowid, * FROM Records_Holders WHERE UPPER(name) like ? OR UPPER(country) like ?', (search, search))
        return self._cursor_to_records_holders(cur)
    except sqlite3.Error as e:
        raise NameError(f'Error searching for name with search term {term}') from e


def update_catches(self, catche):
            """ Updates the Records_Holders tables and removes a name. Raises NameError if name not in database. """
            try:
                with self._db as db:
                    cur = db.cursor()
                    cur.execute('DELETE FROM Records_Holders catche rowid = ?', (catche.id,))
                    if not cur.rowcount:
                     raise CatchError('Tried to delete a catch that doesn\'t exist')
            except sqlite3.Error as e:
                raise CatchError('Error deleting name') from e












