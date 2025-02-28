Assignment-1
from enum import Enum

# Enum for Account Status
class AccountStatus(Enum):
    ACTIVE = "active"
    INACTIVE = "inactive"
    LOCKED = "locked"

# Enum for Order Status
class OrderStatus(Enum):
    PLACED = "placed"
    SHIPPED = "shipped"
    DELIVERED = "delivered"

# Enum for Payment Status
class PaymentStatus(Enum):
    SUCCESS = "success"
    FAILED = "failed"
    REFUNDED = "refunded"

# Enum for Delivery Status
class DeliveryStatus(Enum):
    PENDING = "pending"
    OUT_FOR_DELIVERY = "out_for_delivery"
    DELIVERED = "delivered"


class Customer:
    """
    Customer class represents a customer within the system.
    It includes attributes like username, password, and account status.
    """

    def __init__(self, username, password, account_status):
        """
        Initializes the customer object with username, password, and account status.
        
        :param username: str - the customer's username
        :param password: str - the customer's password
        :param account_status: AccountStatus - the customer's account status (active, inactive, locked)
        """
        self.__username = username         # Private attribute
        self.__password = password         # Private attribute
        self.__account_status = account_status  # Private attribute

    # Getter for username
    def get_username(self):
        return self.__username

    # Setter for username
    def set_username(self, username):
        self.__username = username

    # Getter for password
    def get_password(self):
        return self.__password

    # Setter for password
    def set_password(self, password):
        self.__password = password

    # Getter for account_status
    def get_account_status(self):
        return self.__account_status

    # Setter for account_status
    def set_account_status(self, account_status):
        self.__account_status = account_status

    def login(self):
        """
        Validates the customer's login.
        
        :return: str - login message
        """
        if self.__account_status == AccountStatus.ACTIVE:
            return f"Customer {self.__username} logged in successfully."
        else:
            return "Account is inactive. Please contact support."

    def __str__(self):
        return f"Customer(username={self.__username}, account_status={self.__account_status.value})"


class Order:
    """
    Order class represents a customer's order in the system.
    It includes attributes like order ID, items, total amount, and order status.
    """

    def __init__(self, order_id, items, total_amount, status):
        """
        Initializes the order object with order ID, items, total amount, and status.
        
        :param order_id: str - the unique ID of the order
        :param items: list - the list of items in the order
        :param total_amount: float - the total amount for the order
        :param status: OrderStatus - the current status of the order (placed, shipped, delivered)
        """
        self.__order_id = order_id          # Private attribute
        self.__items = items                # Private attribute
        self.__total_amount = total_amount  # Private attribute
        self.__status = status              # Private attribute

    # Getter for order_id
    def get_order_id(self):
        return self.__order_id

    # Setter for order_id
    def set_order_id(self, order_id):
        self.__order_id = order_id

    # Getter for items
    def get_items(self):
        return self.__items

    # Setter for items
    def set_items(self, items):
        self.__items = items

    # Getter for total_amount
    def get_total_amount(self):
        return self.__total_amount

    # Setter for total_amount
    def set_total_amount(self, total_amount):
        self.__total_amount = total_amount

    # Getter for status
    def get_status(self):
        return self.__status

    # Setter for status
    def set_status(self, status):
        self.__status = status

    def place_order(self):
        """
        Places a new order by updating the order status to 'placed'.
        
        :return: str - order placed message
        """
        self.__status = OrderStatus.PLACED
        return f"Order {self.__order_id} has been placed."

    def update_status(self, new_status):
        """
        Updates the status of the order.
        
        :param new_status: OrderStatus - the new status of the order
        :return: str - status update message
        """
        self.__status = new_status
        return f"Order {self.__order_id} status updated to {self.__status.value}."

    def __str__(self):
        return f"Order(order_id={self.__order_id}, items={self.__items}, total_amount={self.__total_amount}, status={self.__status.value})"


class Payment:
    """
    Payment class represents the payment processing for an order.
    It includes attributes like payment ID, payment method, amount, and payment status.
    """

    def __init__(self, payment_id, payment_method, amount, status):
        """
        Initializes the payment object with payment ID, payment method, amount, and status.
        
        :param payment_id: str - the unique ID for the payment
        :param payment_method: str - the method used for payment (e.g., 'credit_card', 'PayPal')
        :param amount: float - the amount paid
        :param status: PaymentStatus - the payment status (success, failed, refunded)
        """
        self.__payment_id = payment_id      # Private attribute
        self.__payment_method = payment_method  # Private attribute
        self.__amount = amount              # Private attribute
        self.__status = status              # Private attribute

    # Getter for payment_id
    def get_payment_id(self):
        return self.__payment_id

    # Setter for payment_id
    def set_payment_id(self, payment_id):
        self.__payment_id = payment_id

    # Getter for payment_method
    def get_payment_method(self):
        return self.__payment_method

    # Setter for payment_method
    def set_payment_method(self, payment_method):
        self.__payment_method = payment_method

    # Getter for amount
    def get_amount(self):
        return self.__amount

    # Setter for amount
    def set_amount(self, amount):
        self.__amount = amount

    # Getter for status
    def get_status(self):
        return self.__status

    # Setter for status
    def set_status(self, status):
        self.__status = status

    def process_payment(self):
        """
        Processes the payment.
        
        :return: str - payment processed message
        """
        if self.__status == PaymentStatus.SUCCESS:
            return f"Payment {self.__payment_id} processed successfully."
        else:
            return "Payment failed. Please try again."

    def refund(self):
        """
        Refunds the payment if it was successful.
        
        :return: str - refund status message
        """
        if self.__status == PaymentStatus.SUCCESS:
            self.__status = PaymentStatus.REFUNDED
            return f"Payment {self.__payment_id} has been refunded."
        else:
            return "Refund cannot be processed."

    def __str__(self):
        return f"Payment(payment_id={self.__payment_id}, payment_method={self.__payment_method}, amount={self.__amount}, status={self.__status.value})"


class Delivery:
    """
    Delivery class represents the delivery of an order.
    It includes attributes like delivery ID, delivery status, and estimated time.
    """

    def __init__(self, delivery_id, delivery_status, estimated_time):
        """
        Initializes the delivery object with delivery ID, delivery status, and estimated time.
        
        :param delivery_id: str - the unique ID for the delivery
        :param delivery_status: DeliveryStatus - the status of the delivery (pending, out_for_delivery, delivered)
        :param estimated_time: str - the estimated delivery time
        """
        self.__delivery_id = delivery_id         # Private attribute
        self.__delivery_status = delivery_status # Private attribute
        self.__estimated_time = estimated_time   # Private attribute

    # Getter for delivery_id
    def get_delivery_id(self):
        return self.__delivery_id

    # Setter for delivery_id
    def set_delivery_id(self, delivery_id):
        self.__delivery_id = delivery_id

    # Getter for delivery_status
    def get_delivery_status(self):
        return self.__delivery_status

    # Setter for delivery_status
    def set_delivery_status(self, delivery_status):
        self.__delivery_status = delivery_status

    # Getter for estimated_time
    def get_estimated_time(self):
        return self.__estimated_time

    # Setter for estimated_time
    def set_estimated_time(self, estimated_time):
        self.__estimated_time = estimated_time

    def track_delivery(self):
        """
        Tracks the delivery status.
        
        :return: str - delivery tracking message
        """
        return f"Delivery {self.__delivery_id} is {self.__delivery_status.value}. Estimated time: {self.__estimated_time}."

    def assign_agent(self, agent_name):
        """
        Assigns a delivery agent to the order.
        
        :param agent_name: str - name of the assigned agent
        :return: str - assignment confirmation
        """
        return f"Delivery {self.__delivery_id} has been assigned to {agent_name}."

    def __str__(self):
        return f"Delivery(delivery_id={self.__delivery_id}, delivery_status={self.__delivery_status.value}, estimated_time={self.__estimated_time})"


# Test the Classes

customer1 = Customer("john_doe", "password123", AccountStatus.ACTIVE)
order1 = Order("ORD12345", ["item1", "item2"], 250.00, OrderStatus.PLACED)
payment1 = Payment("PAY12345", "credit_card", 250.00, PaymentStatus.SUCCESS)
delivery1 = Delivery("DEL12345", DeliveryStatus.OUT_FOR_DELIVERY, "2:00 PM")

# Print the object details using __str__ method
print(customer1)
print(order1)
print(payment1)
print(delivery1)

# Call methods on objects
print(customer1.login())
print(order1.place_order())
print(payment1.process_payment())
print(delivery1.track_delivery())
