![Matplotlib Layers](https://github.com/sourceduty/Matplotlib_Layers/assets/123030236/952ecb81-0138-4cb5-971f-510927a3bb7e)

> Overlay multiple plots or graphical elements on a single figure using Matplotlib.

#

The objective of the new layers function for the Matplotlib library is to enable users to overlay multiple plots or graphical elements on a single figure. This function will manage the z-order (stacking order) of the elements, allowing for easy customization and manipulation of each layer.

#
##### Function Signature

```
def layers(layers_data, axis=None, order=None, show=True, save_path=None, **kwargs):
    """
    Overlay multiple plots or graphical elements on a single figure.
    
    Parameters:
    - layers_data (list of dicts): List of dictionaries containing data and type of plot.
    - axis (matplotlib.axes.Axes, optional): The axis on which to plot the layers. If None, a new axis is created.
    - order (list of int, optional): The order in which to stack the layers. If None, layers are stacked in the order provided.
    - show (bool, optional): Whether to display the plot. Default is True.
    - save_path (str, optional): Path to save the figure. If None, the figure is not saved.
    - **kwargs: Additional keyword arguments for plot customization.
    
    Returns:
    - matplotlib.figure.Figure: The figure object containing the layered plot.
    - matplotlib.axes.Axes: The axis object containing the layered plot.
    """
```

#
##### Parameters

- layers_data: list of dicts

- A list where each element is a dictionary containing data and parameters for a specific plot.
  
- Each dictionary should include:

- type: str - The type of plot ("line", "scatter", "bar", etc.).
- data: dict - The data for the plot, typically including x and y keys with corresponding data lists.
- kwargs: dict (optional) - Additional keyword arguments for the specific plot type (e.g., color, label, etc.).

- axis: matplotlib.axes.Axes, optional

- The axis on which to plot the layers. If None, a new axis is created.

- order: list of int, optional

- The order in which to stack the layers. If None, layers are stacked in the order provided in layers_data.

- show: bool, optional
- Whether to display the plot. Default is True.

- save_path: str, optional

- Path to save the figure. If None, the figure is not saved.

- kwargs: Additional keyword arguments for plot customization that apply to all layers (e.g., title, xlabel, ylabel, etc.).

#
##### Returns

- matplotlib.figure.Figure
- The figure object containing the layered plot.

- matplotlib.axes.Axes
- The axis object containing the layered plot.

#
##### Testing

To ensure the layers function works as intended, comprehensive testing should be performed. This includes unit tests to validate the functionality with various types of plots and parameters, as well as testing edge cases such as:

- Empty layers_data
- Invalid order indices
- Different plot customizations and styles

#
##### Documentation

Detailed documentation should be provided to guide users on how to use the layers function. This documentation should include:

- Descriptions of each parameter and their expected inputs
- Multiple usage examples with different plot types and customizations
- Explanations of the return values
- Potential use cases and best practices

The layers function should be integrated into the Matplotlib library's official documentation, complete with visual aids and examples, to help users understand and utilize this powerful tool for creating layered plots.

#
##### Example Code

```
import matplotlib.pyplot as plt

def layers(layers_data, axis=None, order=None, show=True, save_path=None, **kwargs):
    """
    Overlay multiple plots or graphical elements on a single figure.
    
    Parameters:
    - layers_data (list of dicts): List of dictionaries containing data and type of plot.
    - axis (matplotlib.axes.Axes, optional): The axis on which to plot the layers. If None, a new axis is created.
    - order (list of int, optional): The order in which to stack the layers. If None, layers are stacked in the order provided.
    - show (bool, optional): Whether to display the plot. Default is True.
    - save_path (str, optional): Path to save the figure. If None, the figure is not saved.
    - **kwargs: Additional keyword arguments for plot customization.
    
    Returns:
    - matplotlib.figure.Figure: The figure object containing the layered plot.
    - matplotlib.axes.Axes: The axis object containing the layered plot.
    """
    
    # Create figure and axis if not provided
    if axis is None:
        fig, ax = plt.subplots()
    else:
        ax = axis
        fig = ax.figure

    # Determine the order of layers
    if order is None:
        order = range(len(layers_data))

    # Add each layer
    for idx in order:
        layer = layers_data[idx]
        plot_type = layer.get("type")
        data = layer.get("data")
        plot_kwargs = layer.get("kwargs", {})
        plot_kwargs.update(kwargs)

        if plot_type == "line":
            ax.plot(data["x"], data["y"], **plot_kwargs)
        elif plot_type == "scatter":
            ax.scatter(data["x"], data["y"], **plot_kwargs)
        elif plot_type == "bar":
            ax.bar(data["x"], data["y"], **plot_kwargs)
        # Add other plot types as needed

    # Show the plot
    if show:
        plt.show()

    # Save the figure if a path is provided
    if save_path:
        fig.savefig(save_path)

    return fig, ax

# Example usage of the layers function
layers_data = [
    {"type": "line", "data": {"x": [1, 2, 3], "y": [4, 5, 6]}, "kwargs": {"color": "blue", "label": "Line Plot"}},
    {"type": "scatter", "data": {"x": [1, 2, 3], "y": [6, 5, 4]}, "kwargs": {"color": "red", "label": "Scatter Plot"}},
    {"type": "bar", "data": {"x": [1, 2, 3], "y": [5, 6, 7]}, "kwargs": {"color": "green", "label": "Bar Plot"}}
]

fig, ax = layers(layers_data, order=[2, 0, 1], show=False)

# Customizing the plot further
ax.set_title("Layered Plot Example")
ax.set_xlabel("X-Axis")
ax.set_ylabel("Y-Axis")
ax.legend()

plt.show()
```

***
Copyright (C) 2024, Sourceduty - All Rights Reserved.
