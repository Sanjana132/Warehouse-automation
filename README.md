# Warehouse-automation
Setting up some input parameters:

Import necessary libraries:
●	Numpy - For numerical operations and Data Manipulation
●	Networkx - For working with Graphs
●	Datetime - For dealing with date and time
●	Random - For generating random values

Inputs are being taken from the user for the following parameters:
●	N : Number of robots
●	L : Length of the Grid
●	W : Width of the grid
●	P : Number of packing stations (<5)

Grid Graph Generation and Visualization:

This script generates a grid graph using NetworkX, adds delivery and supply nodes to the grid, and visualizes the resulting graph using Matplotlib.
This 2D grid graph acts as the warehouse grid and the dimensions of this grid can be inputted by the user. Distance between each node is 1m in all dimensions.
In this grid, each node of the graph is given a node_id and these ids are used to generate orders and assign packing stations.

Order and Robot Classes:

This module defines two classes, ‘Order’ and ‘Robot’, used in a system for managing orders and robots. The ‘Order’ class represents an order, including its number, time of order, items, and available packing stations. The ‘Robot’ class represents a robot for Mode 2 of order fulfillment, including its unique ID, the list of items it will pick, its current position, and the completion time of each item in the order.

Task 1:

Variables:
●	orders (list): A list to store the generated orders. 
●	start_time (datetime): The start time of the simulation created using datetime.now(). 
●	end_time (datetime): The end time of the simulation which is 1 hour after the start _time created using timedelta function.
●	order_time (datetime): The time of each order generation which is generated using np.random.normal()  using the given mean and variance. 
●	order_num (int): A unique order number for each order.
●	item_list_size (int): A random number ranging from 1 to length of supply nodes list using np.random.normal using the given mean and variance.
●	item_list (list): A list containing  item_list_size number of supply nodes using random.sample().
●	num_packing_stations (int) : Number of packing stations for each order based on circular distribution.
●	packing_stations (list): A list containing num_packing_stations number of delivery nodes using random.sample().
An order object is created and order_num, order_time, item_list, packing_stations are added.

Task 2:

Assumption : For both the modes it is assumed that the orders are completed parallelly.

Mode 1:
Using the nx.shortest_path_length() function, we calculate the distance between the start node and node associated with the first item and then we loop through the item list and use the above function for the distance between each item . Finally, we calculate the distance between the last item and the packing station.
Functionalities : The packing station where the order is packed is chosen by taking the node which has the smallest distance from the last item node.

Mode 2: 
In this mode a robot class is used for multiple robots to complete an order. Robot class is created containing an id, item_list, , current_position and competion_time for each robot. For every order, each of these robots gets items appended to their item_list in a circular method. After the items are assigned, for each robot, we iterate through the item_list assigned to that robot and calculate the distance between the robot's current position and that item. Then we calculate the distance between the item and the closest packing station. After an item is packed we update the robots current position and the time when the second item is assigned to the robot. This process continues for all the robots until all items get packed. Then we move to the next order.

Dependencies :
pip install numpy 
pip install matplotlib
pip install networkx
