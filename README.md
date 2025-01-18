// TakingTurnsQueue Implementation
using System;
using System.Collections.Generic;

public class TakingTurnsQueue
{
    private Queue<(string person, int turns)> queue = new Queue<(string, int)>();

    // Add a person to the queue
    public void AddPerson(string person, int turns)
    {
        queue.Enqueue((person, turns));
    }

    // Get the next person and handle re-enqueuing
    public string GetNextPerson()
    {
        if (queue.Count == 0)
            throw new InvalidOperationException("Queue is empty.");

        var (person, turns) = queue.Dequeue();

        if (turns <= 0 || turns > 1)
        {
            queue.Enqueue((person, turns > 0 ? turns - 1 : turns));
        }

        return person;
    }
}

// PriorityQueue Implementation
public class PriorityQueue<T>
{
    private List<(T value, int priority)> items = new List<(T, int)>();

    // Add an item with a priority
    public void Enqueue(T value, int priority)
    {
        items.Add((value, priority));
    }

    // Remove and return the item with the highest priority
    public T Dequeue()
    {
        if (items.Count == 0)
            throw new InvalidOperationException("Queue is empty.");

        // Find the item with the highest priority
        int highestPriorityIndex = 0;
        for (int i = 1; i < items.Count; i++)
        {
            if (items[i].priority > items[highestPriorityIndex].priority)
            {
                highestPriorityIndex = i;
            }
        }

        // Remove and return the item with the highest priority
        var highestPriorityItem = items[highestPriorityIndex];
        items.RemoveAt(highestPriorityIndex);
        return highestPriorityItem.value;
    }
}
