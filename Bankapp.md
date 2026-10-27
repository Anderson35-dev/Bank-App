#include <stdio.h>
#include <stdbool.h>
#include <string.h>
#include <ctype.h>
#include <time.h>
#include <assert.h>

#define SIZE_OF_NAME_BUFFER 20
#define SIZE_OF_USER 50
#define SIZE_OF_NUMBER 11

enum currency
{
    NAIRA,
    DOLLAR,
    POUND,
};

enum transcation_type
{
    CREDIT,
    DEBIT,
    RECHARGE_CARD
};

struct account
{
    int id;
    char account_number[20];
    float balance;
    enum currency currency_type;
};

struct transact
{
    char date[30];
    int user_id;
    int id;
    int amount;
    char account_num[20];
    enum transcation_type type;
};

struct User_Details
{
    char First_Name[SIZE_OF_NAME_BUFFER];
    char Middle_Name[SIZE_OF_NAME_BUFFER];
    char Last_Name[SIZE_OF_NAME_BUFFER];
    char Nin_Bvn[SIZE_OF_NUMBER];
    char Phone_Number[SIZE_OF_NUMBER];
    char Password[SIZE_OF_NUMBER];
    int id;
};

const struct User_Details dummy_user = {
    .First_Name = "John",
    .Middle_Name = "Doe",
    .Last_Name = "Smith",
    .Nin_Bvn = "12345678901",
    .Phone_Number = "08012345678",
    .Password = "password123",
    .id = 1};

static const char *currency_enum_to_string(enum currency type_)
{
    switch (type_)
    {
    case NAIRA:
        return "NAIRA";
    case DOLLAR:
        return "DOLLAR";
    case POUND:
        return "POUND";

    default:
        return "UNKNOWN CURRENCY";
    }
}
static const char *transaction_type_enum_to_string(enum transcation_type type)
{
    switch (type)
    {
    case CREDIT:
        return "CREDIT";
    case DEBIT:
        return "DEBIT";
    case RECHARGE_CARD:
        return "RECHARGE_CARD";

    default:
        return "UNKNOWN TRANSACTION";
    }
}

static void print_user(struct User_Details details)
{
    printf("\nUSER DETAILS\n");
    printf("First Name: %s\n", details.First_Name);
    printf("Middle Name: %s\n", details.Middle_Name);
    printf("Last Name: %s\n", details.Last_Name);
    printf("Phone Number: %s\n", details.Phone_Number);
    printf("Password: %s\n\n", details.Password);
}

static void print_transaction(struct transact transaction)
{
    printf("\nTRANSACTION DETAILS\n");
    printf("Transaction ID: %d\n", transaction.id);
    printf("User ID: %d\n", transaction.user_id);
    printf("Account Number: %s\n", transaction.account_num);
    printf("Amount: %d\n", transaction.amount);
    printf("Type: %s\n\n", transaction_type_enum_to_string(transaction.type));
    printf("Date: %s\n", transaction.date);
}

static void print_account(struct account account)
{
    printf("\nACCOUNT DETAILS\n");
    printf("Account ID: %d\n", account.id);
    printf("Account Number: %s\n", account.account_number);
    printf("Balance: %.2f\n\n", account.balance);
    printf("Currency Type: %s\n", currency_enum_to_string(account.currency_type));
}

bool register_account(struct account account_array[0], struct account account_details)
{
    assert(account_array != NULL);
    assert(account_details.id > 0);

    for (int i = 0; i < SIZE_OF_USER; i++)
    {
        if (account_array[i].id == 0)
        {
            account_array[i] = account_details;
            return true;
        }
    }
    return false;
}

bool read_account(struct account account_array[], int id, struct account *account_details)
{
    assert(account_array != NULL);
    assert(id > 0);
    assert(account_details != NULL);

    for (int i = 0; i < SIZE_OF_USER; i++)
    {
        if (account_array[i].id == id)
        {
            *account_details = account_array[i];
            return true;
        }
    }
    return false;
}

bool update_account(struct account account_array[], struct account account_details, int id)
{
    assert(account_array != NULL);
    assert(account_details.id > 0);

    for (int i = 0; i < SIZE_OF_USER; i++)
    {
        if (account_array[i].id == id)
        {
            account_array[i] = account_details;
            return true;
        }
    }
    return false;
}

bool delete_account(struct account account_array[], int id)
{
    assert(account_array != NULL);
    assert(id > 0);

    for (int i = 0; i < SIZE_OF_USER; i++)
    {
        if (account_array[i].id == id)
        {
            account_array[i].id = 0;
            return true;
        }
    }
    return false;
}

bool register_transaction(struct transact transaction_array[], struct transact transaction)
{
    for (int i = 0; i < SIZE_OF_USER; i++)
    {
        if (transaction_array[i].id == 0)
        {
            transaction_array[i] = transaction;
            return true;
        }
    }
    return false;
}

bool read_transaction(struct transact transaction_array[], int id, struct transact *transaction_details)
{
    bool found = false;
    for (int i = 0; i < SIZE_OF_USER; i++)
    {
        if (transaction_array[i].id == id)
        {
            *transaction_details = transaction_array[i];
            found = true;
        }
    }
    return found;
}

bool update_transcation(struct transact transcation_array[], struct transact transcation, int id)
{
    for (int i = 0; i < SIZE_OF_USER; i++)
    {
        if (transcation_array[i].id == id)
        {
            transcation_array[i] = transcation;
            return true;
        }
    }
    return false;
}

bool delete_transcation(struct transact transaction_array[], int id)
{
    for (int i = 0; i < SIZE_OF_USER; i++)
    {
        if (transaction_array[i].id == id)
        {
            transaction_array[i].id = 0;
            return true;
        }
    }
    return false;
}
bool Is_Number(char number[])
{
    for (int i = 0; number[i] != '\0'; i++)
    {
        if (!isdigit((unsigned char)number[i]))
        {
            return false;
        }
    }
    return true;
}

bool Is_Alphabet(char name[])
{
    for (int i = 0; name[i] != '\0'; i++)
    {
        if (!isalpha((unsigned char)name[i]))
        {
            return false;
        }
    }
    return true;
}

bool Register_User(struct User_Details user_array[], struct User_Details bank)
{
    for (int i = 0; i < SIZE_OF_USER; i++)
    {
        if (user_array[i].id == 0)
        {
            user_array[i] = bank;
            return true;
        }
    }
    return false;
}

bool Update_User(struct User_Details user_array[], struct User_Details bank)
{
    for (int i = 0; i < SIZE_OF_USER; i++)
    {
        if (user_array[i].id == bank.id)
        {
            user_array[i] = bank;
            return true;
        }
    }
    return false;
}

bool Read_User(struct User_Details user_array[], int id, struct User_Details *user_details)
{
    for (int i = 0; i < SIZE_OF_USER; i++)
    {
        if (user_array[i].id == id)
        {
            *user_details = user_array[i];
            return true;
        }
    }
    return false;
}

bool Delete_User(struct User_Details user_array[], int id)
{
    for (int i = 0; i < SIZE_OF_USER; i++)
    {
        if (user_array[i].id == id)
        {
            user_array[i].id = 0;
            return true;
        }
    }
    return false;
}

int main()
{
    struct User_Details user_array[SIZE_OF_USER] = {0};
    struct User_Details bank;
    struct transact transaction_array[SIZE_OF_USER] = {0};
    struct transact transaction;
    struct account account_array[SIZE_OF_USER] = {0};
    struct account account_details;
    struct tm *ptr;
    time_t t;
    t = time(NULL);
    ptr = localtime(&t);
    strcpy(transaction.date, asctime(ptr));

    int choice;
    static int user_store_index = 1;
    static int transaction_store_index = 1;

    int id = 0;
    int user_id = 0;
    int currency_type;
    char account_num[20];

    printf("WELCOME TO ANDERSONBANK\n\n");

    while (1)
    {

        printf("Enter 1 to Register user\n");
        printf("Enter 2 to Update user\n");
        printf("Enter 3 to Read user\n");
        printf("Enter 4 to Delete user\n");
        printf("Enter 5 to Transact\n");
        printf("Enter 6 to Read Transaction\n");
        printf("Enter 7 to Update Transaction\n");
        printf("Enter 8 to Delete Transcation\n");
        printf("Enter 9 to Use Dummy User Data\n");
        printf("Enter 10 to Register Account\n");
        printf("Enter 11 to Read Account\n");
        printf("Enter 12 to Update Account\n");
        printf("Enter 13 to Delete Account\n");
        printf("Choice: ");
        scanf("%d", &choice);

        if (choice == 1)
        {
            while (1)
            {
                printf("Enter Your First Name: ");
                scanf("%s", bank.First_Name);
                if (strlen(bank.First_Name) >= SIZE_OF_NAME_BUFFER)
                {
                    printf("\nError, Name Should not be more than 20 character\n");
                }
                else if (!Is_Alphabet(bank.First_Name))
                {
                    printf("\nInvalid, enter Alphabet only\n\n");
                }
                else
                {
                    break;
                }
            }
            while (1)
            {
                printf("Enter Your Middle Name: ");
                scanf("%s", bank.Middle_Name);
                if (strlen(bank.Middle_Name) >= SIZE_OF_NAME_BUFFER)
                {
                    printf("\nError, Name Should not be more than 20 character\n");
                }
                else if (!Is_Alphabet(bank.Middle_Name))
                {
                    printf("\nInvalid, enter Alphabet only\n\n");
                }
                else
                {
                    break;
                }
            }
            while (1)
            {
                printf("Enter Your Last Name: ");
                scanf("%s", bank.Last_Name);
                if (strlen(bank.Last_Name) >= SIZE_OF_NAME_BUFFER)
                {
                    printf("\nError, Name Should not be more than 20 character\n");
                }
                else if (!Is_Alphabet(bank.Last_Name))
                {
                    printf("\nInvalid, enter Alphabet only\n\n");
                }
                else
                {
                    break;
                }
            }
            while (1)
            {
                printf("Enter Your Nin/Bvn: ");
                scanf("%11s", bank.Nin_Bvn);
                if (strlen(bank.Nin_Bvn) > SIZE_OF_NUMBER)
                {
                    printf("\nError, Number Should not be more than 11 Characters\n\n");
                }
                else if (strlen(bank.Nin_Bvn) < SIZE_OF_NUMBER)
                {
                    printf("\nError, Number Should not be less than 11 Characters\n\n");
                }
                else if (!Is_Number(bank.Nin_Bvn))
                {
                    printf("\nInvalid, enter Number only\n\n");
                }
                else
                {
                    break;
                }
            }
            while (1)
            {
                printf("Enter Your Phone Number: ");
                scanf("%11s", bank.Phone_Number);
                if (strlen(bank.Phone_Number) > SIZE_OF_NUMBER)
                {
                    printf("\nError, Number Should not be more than 11 Character\n\n");
                }
                else if (strlen(bank.Phone_Number) < SIZE_OF_NUMBER)
                {
                    printf("\nError, Number Should not be less than 11 Characters\n\n");
                }
                else if (!Is_Number(bank.Phone_Number))
                {
                    printf("\nInvalid, enter Number only\n\n");
                }
                else
                {
                    break;
                }
            }

            printf("Enter Password: ");
            scanf("%s", bank.Password);

            bank.id = user_store_index;
            printf("Your ID is: %d\n", bank.id);

            if (Register_User(user_array, bank))
            {
                user_store_index++;
                printf("\nUSER REGISTERED SUCCESSFULLY\n\n");
            }
            else
            {
                printf("\nREGISTRATION FAILED, Bank system is full\n\n");
            }
        }

        else if (choice == 2)
        {
            printf("Enter your ID to update: ");
            scanf("%d", &bank.id);

            if (!Read_User(user_array, bank.id, &bank))
            {
                printf("\nUser Not Found\n\n");
            }
            else
            {
                while (1)
                {
                    printf("Enter Your New First Name: ");
                    scanf("%19s", bank.First_Name);

                    if (!Is_Alphabet(bank.First_Name))
                    {
                        printf("Invalid, enter Alphabet only\n");
                    }
                    else
                    {
                        break;
                    }
                }

                while (1)
                {
                    printf("Enter Your New Middle Name: ");
                    scanf("%19s", bank.Middle_Name);

                    if (!Is_Alphabet(bank.Middle_Name))
                    {
                        printf("Invalid, enter Alphabet only\n");
                    }
                    else
                    {
                        break;
                    }
                }

                while (1)
                {
                    printf("Enter Your New Last Name: ");
                    scanf("%19s", bank.Last_Name);

                    if (!Is_Alphabet(bank.Last_Name))
                    {
                        printf("Invalid, enter Alphabet only\n");
                    }
                    else
                    {
                        break;
                    }
                }

                while (1)
                {
                    printf("Enter Your Phone Number: ");
                    scanf("%11s", bank.Phone_Number);

                    if (strlen(bank.Phone_Number) != 11 ||
                        !Is_Number(bank.Phone_Number))
                    {
                        printf("Invalid phone number. Enter 11 digits.\n");
                    }
                    else
                    {
                        break;
                    }
                }

                printf("Enter your New Password: ");
                scanf("%s", bank.Password);

                if (Update_User(user_array, bank))
                {
                    printf("\nUser Updated Successfully\n\n");
                }
                else
                {
                    printf("\nUser Not Found\n\n");
                }
            }
        }
        else if (choice == 3)
        {
            printf("Enter User ID: ");
            scanf("%d", &id);
            if (!Read_User(user_array, bank.id, &bank))
            {
                printf("\nUser Not Found\n\n");
            }
            else
            {
                if (!Read_User(user_array, id, &bank))
                {
                    printf("\nUser Not Found\n\n");
                }
                print_user(bank);
            }
        }

        else if (choice == 4)
        {
            printf("Enter Your ID to Delete: ");
            scanf("%d", &id);
            if (!Read_User(user_array, bank.id, &bank))
            {
                printf("\nUser Not Found\n\n");
            }
            else
            {
                if (Delete_User(user_array, id))
                {
                    printf("\nAccount Deleted Successfully\n\n");
                }
                else
                {
                    printf("\nUser Not Found\n\n");
                }
            }
        }

        else if (choice == 5)
        {
            while (1)
            {
                printf("Enter Your ID to Transact: ");
                scanf("%d", &transaction.user_id);
                bool result = Read_User(user_array, transaction.user_id, &bank);
                if (!result)
                {
                    printf("\nUser Not Found\n\n");
                    continue;
                }
                printf("Enter Amount: ");
                scanf("%d", &transaction.amount);
                printf("Enter the transaction type (0 for CREDIT, 1 for DEBIT, 2 for RECHARGE_CARD): ");
                int type;
                scanf("%d", &type);
                if (type < 0 || type > 2)
                {
                    printf("\nInvalid transaction type. Please enter 0, 1, or 2.\n\n");
                    continue;
                }
                transaction.type = (enum transcation_type)type;
                transaction.user_id = bank.id;
                strncpy(transaction.account_num, bank.Phone_Number, SIZE_OF_NUMBER);
                transaction.id = transaction_store_index;
                transaction_store_index++;
                print_transaction(transaction);
                if (register_transaction(transaction_array, transaction))
                {
                    printf("\nTransaction Successfully, You transfer the amount of %d\n", transaction.amount);
                    printf("Date of Transaction: %s\n\n", &transaction.date);
                }
                else
                {
                    printf("\nTransaction Failed, Bank system is full\n\n");
                }
                break;
            }
        }

        else if (choice == 6)
        {
            printf("Enter Your ID to Read Transaction: ");
            scanf("%d", &user_id);
            if (!read_transaction(transaction_array, user_id, &transaction))
            {
                printf("\nTransaction Not Found\n\n");
            }
            else
            {
                print_transaction(transaction);
            }
        }

        else if (choice == 7)
        {
            printf("Enter the ID of transaction to update: ");
            int transaction_id;
            scanf("%d", &transaction_id);
            if (!read_transaction(transaction_array, transaction_id, &transaction))
            {
                printf("\nTransaction Not Found\n\n");
                continue;
            }
            printf("Enter new transaction details:\n");
            scanf("%d", &transaction.user_id);
            printf("Enter Account Number: ");
            scanf("%s", transaction.account_num);
            printf("Enter New Amount: ");
            scanf("%d", &transaction.amount);
            if (update_transcation(transaction_array, transaction, transaction_id))
            {
                printf("\nTransaction Updated Successfully\n\n");
            }
            else
            {
                printf("\nTransaction Not Found\n\n");
            }
        }

        else if (choice == 8)
        {
            printf("Enter the ID of transaction to delete: ");
            int transaction_id;
            scanf("%d", &transaction_id);
            if (delete_transcation(transaction_array, transaction_id))
            {
                printf("\nTransaction Deleted Successfully\n\n");
            }
            else
            {
                printf("\nTransaction Not Found\n\n");
            }
        }
        else if (choice == 9)
        {
            printf("\nUse dummy user data\n");
            if (Register_User(user_array, dummy_user))
            {
                user_store_index++;
                printf("\n DUMMY USER REGISTERED SUCCESSFULLY\n\n");
                print_user(dummy_user);
                print_user(user_array[0]);
            }
            else
            {
                printf("\nDUMMY REGISTRATION FAILED, Bank system is full\n\n");
            }
        }

        else if (choice == 10)
        {
            printf("Enter Account ID: ");
            scanf("%d", &account_details.id);
            if (!Read_User(user_array, bank.id, &bank))
            {
                printf("\nUser Not Found\n\n");
            }
            else
            {
                printf("Enter Account Number: ");
                scanf("%s", account_details.account_number);
                printf("Enter Balance: ");
                scanf("%f", &account_details.balance);
                printf("Enter Currency Type (0 for NAIRA, 1 for DOLLAR, 2 for POUND): ");
                scanf("%d", &currency_type);
                if (currency_type < 0 || currency_type > 2)
                {
                    printf("\nInvalid currency type. Please enter 0, 1, or 2.\n\n");
                    continue;
                }
                account_details.currency_type = (enum currency)currency_type;
                if (register_account(account_array, account_details))
                {
                    printf("\nACCOUNT REGISTERED SUCCESSFULLY\n\n");
                }
                else
                {
                    printf("\nREGISTRATION FAILED, Bank system is full\n\n");
                }
            }
        }

        else if (choice == 11)
        {
            printf("Enter Account ID to Read: ");
            scanf("%d", &id);
            if (!Read_User(user_array, bank.id, &bank))
            {
                printf("\nUser Not Found\n\n");
            }
            else
            {
                if (!read_account(account_array, id, &account_details))
                {
                    printf("\nAccount Not Found\n\n");
                }
                else
                {
                    print_account(account_details);
                }
            }
        }

        else if (choice == 12)
        {
            printf("Enter Account ID to Update: ");
            scanf("%d", &account_details.id);
            if (!Read_User(user_array, bank.id, &bank))
            {
                printf("\nUser Not Found\n\n");
            }
            else
            {
                printf("Enter New Account Number: ");
                scanf("%s", account_details.account_number);
                printf("Enter New Balance: ");
                scanf("%f", &account_details.balance);
                printf("Enter New Currency Type (0 for NAIRA, 1 for DOLLAR, 2 for POUND): ");
                scanf("%d", &currency_type);
                if (currency_type < 0 || currency_type > 2)
                {
                    printf("\nInvalid currency type. Please enter 0, 1, or 2.\n\n");
                    continue;
                }
                account_details.currency_type = (enum currency)currency_type;
                if (update_account(account_array, account_details, account_details.id))
                {
                    printf("\nAccount Updated Successfully\n\n");
                }
                else
                {
                    printf("\nAccount Not Found\n\n");
                }
            }
        }

        else if (choice == 13)
        {
            printf("Enter Account ID to Delete: ");
            scanf("%d", &id);
            if (!Read_User(user_array, bank.id, &bank))
            {
                printf("\nUser Not Found\n\n");
            }
            else
            {
                if (delete_account(account_array, id))
                {
                    printf("\nAccount Deleted Successfully\n\n");
                }
                else
                {
                    printf("\nAccount Not Found\n\n");
                }
            }
        }

        else
        {
            printf("\nInvalid Choice, Please Try Again\n\n");
        }
    }
}
