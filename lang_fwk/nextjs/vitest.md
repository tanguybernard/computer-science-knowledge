

Note :

Quand on veut tester le rendu d'un composant, attendre que celui ci s'affiche avant le expect :


    describe('MyComponent', () => {
      it('devrait afficher un texte après le rendu', async () => {
        render(<MyComponent />); // Render du composant
    
        // Attendre que le texte soit présent dans le DOM
        await waitFor(() => {
          expect(screen.getByText('Texte attendu')).toBeInTheDocument();
        });
      });
    });


ou bien attendre de trouver un élément en particulier puis faire le expect

    // j'attends un tableau
    await screen.findAllByRole('columnheader');
    // Puis je cherche tout les buttons avec ce texte
    const buttons = screen.findAllByText('CGV');
    //assertions    
    expect(buttons[0]).toBeDisabled();
    expect(buttons[0]).not.toBeDisabled();






