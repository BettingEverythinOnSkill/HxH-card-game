# HxH-card-game
using UnityEngine;
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine.UI;
using UnityEngine.EventSystems;


public class Into_Deck : MonoBehaviour
{
    GameObject topcard = null;
    public List<GameObject> deck = new List<GameObject>();
    int old_count;
    GameObject newcard;

    //x is used for getting a card in the position in the list 
    int x;

    Sprite background;

    void Start()
    {
        old_count = this.transform.childCount;
        background = this.GetComponent<Image>().sprite;
    }
    
    void Update ()
    {
        
        if (Input.GetAxis("Mouse ScrollWheel") == 1)
        {

            try
            {
                topcard = deck[x++];
            }
            catch(ArgumentOutOfRangeException)
            {
                topcard = null;
                x = 0;
            }
        }
        
        else if (Input.GetAxis("Mouse ScrollWheel") == -1)
        {
            try
            {
                topcard = deck[x--];
            }
            catch (ArgumentOutOfRangeException)
            {
                topcard = null;
                x = 0;
            }
        }


        if (topcard != null)
        {
            topcard.SetActive(true);
            Active.active_card = topcard.transform;
        }
        
        else
        {
            this.GetComponent<Image>().sprite = background;
        }

        

       if (old_count != this.transform.childCount)
        {
            newcard = this.transform.GetChild(this.transform.childCount - 1).gameObject;
            deck.Add(newcard);
            old_count = this.transform.childCount;
        }
       
        foreach (GameObject x in deck)
        {
            if (x.transform.parent != this.gameObject)
            {
                deck.RemoveAt(deck.BinarySearch(x));
            }
            if (x != topcard)
            { 
                x.SetActive(false);
            }
            
        }
    }
}
