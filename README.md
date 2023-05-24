import random

def create_deck():

    ranks = ['2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K', 'A']

    suits = ['♠', '♣', '♦', '♥']

    deck = [(rank, suit) for rank in ranks for suit in suits]

    random.shuffle(deck)

    return deck

def deal_card(deck):

    card = deck.pop()

    return card

def calculate_score(hand):

    score = 0

    ace_count = 0

    for card in hand:

        rank = card[0]

        if rank.isdigit():

            score += int(rank)

        elif rank in ['J', 'Q', 'K']:

            score += 10

        elif rank == 'A':

            score += 11

            ace_count += 1

    while score > 21 and ace_count > 0:

        score -= 10

        ace_count -= 1

    return score

def compare_scores(player_score, computer_score):

    if player_score > 21 and computer_score > 21:

        return "Tas ir neizšķirts. Pārsniegts 21 punkts."

    if player_score == computer_score:

        return "Neizšķirts."

    elif computer_score == 21:

        return "Dators uzvar ar 21 punktu!"

    elif player_score == 21:

        return "Tu uzvari ar 21 punktu!"

    elif player_score > 21:

        return "Tu zaudēji. Pārsniegts 21 punkts."

    elif computer_score > 21:

        return "Dators zaudē. Pārsniegts 21 punkts."

    elif player_score > computer_score:

        return "Tu uzvari!"

    else:

        return "Dators uzvar!"

def play_game():

    print("Sākam spēli!")

    deck = create_deck()

    player_hand = [deal_card(deck), deal_card(deck)]

    computer_hand = [deal_card(deck), deal_card(deck)]

    game_over = False

    while not game_over:

        player_score = calculate_score(player_hand)

        computer_score = calculate_score(computer_hand)

        print(f"Tavi kartis: {player_hand}, Punkti: {player_score}")

        print(f"Datora karts: {computer_hand[0]}")

        if player_score == 0 or computer_score == 0 or player_score > 21:

            game_over = True

        else:

            should_continue = input("Vai gribi saņemt vēl karti? (jā/nē): ")

            if should_continue.lower() == "jā":

                player_hand.append(deal_card(deck))

            else:

                game_over = True

    while computer_score < 17 and computer_score != 0:

        computer_hand.append(deal_card(deck))

        computer_score = calculate_score(computer_hand)

    print(f"Tavi kartis: {player_hand}, Punkti: {player_score}")

    print(f"Datora kartis: {computer_hand}, Punkti: {computer_score}")

    print(compare_scores(player_score, computer_score))

while input("Gribi spēlēt spēli 'Spēlētājs pret datoru

